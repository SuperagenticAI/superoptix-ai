# Evaluation & Testing Guide

SuperOptiX provides a comprehensive BDD (Behavior-Driven Development) evaluation framework that validates your agents against real-world scenarios. This guide covers how to test and validate your agents effectively.

## What is BDD Evaluation?

BDD evaluation in SuperOptiX uses **feature specifications** (scenarios) to test agent behavior in realistic situations. Each scenario defines:
- **Given**: The context or situation
- **When**: The action or input
- **Then**: The expected behavior or output

This approach ensures your agents perform correctly in real-world scenarios before deployment.

## CLI Command Options

The `super agent evaluate` command provides comprehensive testing capabilities with multiple output formats for different use cases:

### Basic Usage
```bash
# Standard evaluation
super agent evaluate <agent_name>

# Verbose output with detailed results
super agent evaluate <agent_name> --verbose

# Auto-tuning for improved evaluation accuracy
super agent evaluate <agent_name> --auto-tune
```

### Output Formats
```bash
# Table format (default) - Beautiful console output
super agent evaluate <agent_name> --format table

# JSON format - For CI/CD integration and automation
super agent evaluate <agent_name> --format json

# JUnit format - Compatible with CI/CD systems
super agent evaluate <agent_name> --format junit
```

### Report Generation
```bash
# Save detailed report to file
super agent evaluate <agent_name> --save-report test_results.json

# Combine with JSON format for automation
super agent evaluate <agent_name> --format json --save-report results.json
```

### Development Options
```bash
# Ignore non-essential checks for rapid development
super agent evaluate <agent_name> --ignore-checks

# Verbose mode for detailed analysis
super agent evaluate <agent_name> --verbose
```

## CI/CD Integration

### Proper BDD/TDD Workflow

The correct workflow follows BDD/TDD best practices:

#### **Phase 1: Specification-Driven Development**
```bash
# 1. Define BDD scenarios FIRST
vim agents/<agent_name>/Playbook/developer_playbook.yaml
# Add comprehensive feature_specifications

# 2. Compile agent with scenarios
super agent compile developer

# 3. Run baseline evaluation (should show current performance)
super agent evaluate developer
# This gives us baseline metrics before optimization
```

#### **Phase 2: Iterative Improvement**
```bash
# 4. Analyze baseline results
# - Identify failing scenarios
# - Understand performance gaps
# - Plan optimization strategy

# 5. Optimize based on evaluation feedback
super agent optimize developer

# 6. Re-evaluate to measure improvement
super agent evaluate developer

# 7. Iterate until quality gates pass
# Repeat steps 5-6 until pass rate ≥ 80%
```

#### **Phase 3: Production Deployment**
```bash
# 8. Final validation
super agent evaluate developer --verbose

# 9. Deploy only if quality gates pass
super agent run developer --goal "production task"
```

### GitHub Actions Integration

```yaml
# .github/workflows/agent-quality.yml
name: Agent Quality Check
on: [push, pull_request]

jobs:
  bdd-workflow:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Setup Python
        uses: actions/setup-python@v3
        with:
          python-version: '3.11'
      
      - name: Setup SuperOptiX
        run: pip install superoptix
      
      - name: Compile Agent
        run: super agent compile developer
      
      - name: Baseline Evaluation
        run: |
          super agent evaluate developer --format json --save-report baseline.json
          # Check if baseline is acceptable
          pass_rate=$(jq -r '.summary.pass_rate' baseline.json | tr -d '%')
          if (( $(echo "$pass_rate < 40" | bc -l) )); then
            echo "Baseline too low: $pass_rate%"
            exit 1
          fi
      
      - name: Optimize Agent
        run: super agent optimize developer
      
      - name: Final Evaluation
        run: |
          super agent evaluate developer --format json --save-report results.json
          # Quality gate: must improve by at least 20%
          improvement=$(jq -r '.improvement.percentage' results.json | tr -d '%')
          if (( $(echo "$improvement < 20" | bc -l) )); then
            echo "Insufficient improvement: $improvement%"
            exit 1
          fi
      
      - name: Upload Test Results
        uses: actions/upload-artifact@v3
        with:
          name: bdd-spec-results
          path: results.json
```

### GitLab CI Integration

```yaml
# .gitlab-ci.yml
stages:
  - test
  - optimize
  - validate

agent-test:
  stage: test
  image: python:3.11
  script:
    - pip install superoptix
    - super agent compile developer
    - super agent evaluate developer --format json --save-report baseline.json
    - |
      # Extract pass rate for quality gate
      PASS_RATE=$(python -c "
      import json
      with open('baseline.json') as f:
          data = json.load(f)
      print(data['summary']['pass_rate'].replace('%', ''))
      ")
      echo "Pass rate: $PASS_RATE%"
      if [ "$PASS_RATE" -lt 40 ]; then
          echo "Baseline too low: $PASS_RATE%"
          exit 1
      fi
  artifacts:
    reports:
      junit: test-results.xml
    paths:
      - baseline.json

agent-optimize:
  stage: optimize
  image: python:3.11
  script:
    - pip install superoptix
    - super agent optimize developer
  dependencies:
    - agent-test

agent-validate:
  stage: validate
  image: python:3.11
  script:
    - pip install superoptix
    - super agent evaluate developer --format json --save-report final.json
    - |
      # Quality gate check
      IMPROVEMENT=$(python -c "
      import json
      with open('final.json') as f:
          data = json.load(f)
      print(data.get('improvement', {}).get('percentage', '0').replace('%', ''))
      ")
      echo "Improvement: $IMPROVEMENT%"
      if [ "$IMPROVEMENT" -lt 20 ]; then
          echo "Insufficient improvement: $IMPROVEMENT%"
          exit 1
      fi
  dependencies:
    - agent-optimize
```

### Jenkins Pipeline Integration

```groovy
// Jenkinsfile
pipeline {
    agent any
    
    stages {
        stage('Setup') {
            steps {
                sh 'pip install superoptix'
            }
        }
        
        stage('Compile') {
            steps {
                sh 'super agent compile developer'
            }
        }
        
        stage('Baseline Test') {
            steps {
                sh 'super agent evaluate developer --format json --save-report baseline.json'
                script {
                    def baseline = readJSON file: 'baseline.json'
                    def passRate = baseline.summary.pass_rate.replace('%', '').toInteger()
                    if (passRate < 40) {
                        error "Baseline too low: ${passRate}%"
                    }
                }
            }
        }
        
        stage('Optimize') {
            steps {
                sh 'super agent optimize developer'
            }
        }
        
        stage('Final Test') {
            steps {
                sh 'super agent evaluate developer --format json --save-report final.json'
                script {
                    def final = readJSON file: 'final.json'
                    def improvement = final.improvement?.percentage?.replace('%', '')?.toInteger() ?: 0
                    if (improvement < 20) {
                        error "Insufficient improvement: ${improvement}%"
                    }
                }
            }
        }
    }
    
    post {
        always {
            archiveArtifacts artifacts: '*.json', fingerprint: true
            publishTestResults testResultsPattern: 'test-results.xml'
        }
    }
}
```

### Azure DevOps Integration

```yaml
# azure-pipelines.yml
trigger:
  - main

pool:
  vmImage: 'ubuntu-latest'

stages:
- stage: Test
  displayName: 'Agent Testing'
  jobs:
  - job: BDDWorkflow
    steps:
    - task: UsePythonVersion@0
      inputs:
        versionSpec: '3.11'
    
    - script: |
        pip install superoptix
      displayName: 'Install SuperOptiX'
    
    - script: |
        super agent compile developer
      displayName: 'Compile Agent'
    
    - script: |
        super agent evaluate developer --format json --save-report baseline.json
      displayName: 'Baseline Evaluation'
    
    - script: |
        # Check baseline quality gate
        python -c "
        import json
        with open('baseline.json') as f:
            data = json.load(f)
        pass_rate = int(data['summary']['pass_rate'].replace('%', ''))
        if pass_rate < 40:
            exit(1)
        print(f'Baseline pass rate: {pass_rate}%')
        "
      displayName: 'Quality Gate Check'
    
    - script: |
        super agent optimize developer
      displayName: 'Optimize Agent'
    
    - script: |
        super agent evaluate developer --format json --save-report final.json
      displayName: 'Final Evaluation'
    
    - script: |
        # Check improvement quality gate
        python -c "
        import json
        with open('final.json') as f:
            data = json.load(f)
        improvement = int(data.get('improvement', {}).get('percentage', '0').replace('%', ''))
        if improvement < 20:
            exit(1)
        print(f'Improvement: {improvement}%')
        "
      displayName: 'Improvement Check'
    
    - task: PublishTestResults@2
      inputs:
        testResultsFormat: 'JUnit'
        testResultsFiles: 'test-results.xml'
        mergeTestResults: true
        testRunTitle: 'BDD Specifications'
      condition: succeededOrFailed()
    
    - task: PublishBuildArtifacts@1
      inputs:
        PathtoPublish: '*.json'
        ArtifactName: 'TestResults'
        publishLocation: 'Container'
```

### Quality Gates in Scripts

For custom CI/CD scripts, you can implement quality gates:

```bash
#!/bin/bash
# quality-gate.sh

# Set minimum thresholds
MIN_PASS_RATE=80
MIN_IMPROVEMENT=20

# Run evaluation and extract metrics
super agent evaluate developer --format json --save-report results.json

# Extract pass rate
PASS_RATE=$(jq -r '.summary.pass_rate' results.json | tr -d '%')

# Extract improvement percentage
IMPROVEMENT=$(jq -r '.improvement.percentage' results.json | tr -d '%')

echo "Pass Rate: $PASS_RATE%"
echo "Improvement: $IMPROVEMENT%"

# Quality gate checks
if [ "$PASS_RATE" -lt "$MIN_PASS_RATE" ]; then
    echo "❌ Quality gate failed: $PASS_RATE% < $MIN_PASS_RATE%"
    exit 1
fi

if [ "$IMPROVEMENT" -lt "$MIN_IMPROVEMENT" ]; then
    echo "❌ Improvement gate failed: $IMPROVEMENT% < $MIN_IMPROVEMENT%"
    exit 1
fi

echo "✅ All quality gates passed!"
```

## Best Practices

### **✅ DO's**
1. **Always evaluate before optimizing**
2. **Set clear quality gates**
3. **Measure improvement quantitatively**
4. **Iterate based on evaluation feedback**
5. **Use scenarios as both training data and test cases**

### **❌ DON'Ts**
1. **Don't optimize without baseline**
2. **Don't skip evaluation after optimization**
3. **Don't deploy without quality gates**
4. **Don't ignore failing scenarios**

## Troubleshooting

### Common Issues

#### **No BDD Specifications Found**
```
❌ No BDD specifications found!

💡 Solution:
1. Edit your agent playbook YAML file
2. Add 'feature_specifications' section with 'scenarios'
3. Recompile agent: super agent compile developer
```

#### **Low Pass Rates**
```
❌ NEEDS WORK - 30% pass rate

💡 Solutions:
• Run optimization: super agent optimize developer
• Upgrade model: Use llama3.1:8b or GPT-4
• Review specification complexity vs model capabilities
• Improve agent prompts and training data
```

#### **Semantic Similarity Issues**
```
semantic meaning differs significantly

💡 Fix Guidance:
• Make responses more relevant to expected output
• Use similar terminology and concepts
• Address all aspects of the input requirement
• Improve response clarity and structure
```

**🎯 Key Takeaway**: Always evaluate before optimizing. This ensures you have a baseline, can measure improvement, and follow proper BDD/TDD practices for reliable AI agent development. 