# Useful Tools and Resources  
References, Links, and tools for DevSecOps.  
Compiled from and while taking the SANS SEC540 Secure DevOps and Cloud Application Security course

OWASP Infrastructure as Code Security Cheatsheet:
https://cheatsheetseries.owasp.org/cheatsheets/Infrastructure_as_Code_Security_Cheat_Sheet.html


 **The OWASP AppSec Pipeline Project**  

 [Link](https://owasp.org/www-project-appsec-pipeline/)  

 > Provides a framework for building a DevSecOps pipeline for application security  

  **Bag of Holding, by Pearson Education**  

 [Link](https://github.com/aparsons/bag-of-holding)    
 > Application inventory and classification information, and record and manage manual assessments and results with this tool  

 ## Code Inventory  

GitHub Sloc Cloc and Code (SCC)  
> [SCC Github](https://github.com/boyter/scc)  

 ## IDE Static Analysis Tools/Extensions  

[SCode plugins for Semgrep](https://github.com/returntocorp/semgrep)  

[Checkov](https://github.com/bridgecrewio/checkov),   

[cfn_nag](https://github.com/stelligent/cfn_nag)  

[FindBugs plugin for Eclipse](http://findbugs.sourceforge.net/manual/eclipse.html)
[FindBugs plugin for IntelliJ](https://plugins.jetbrains.com/plugin/3847-findbugs-idea)

[SpotBugs plugin for Eclipse](https://spotbugs.github.io/  )  

[Puma Scanopen-source (and commercial) Visual Studio plugin for C#](https://pumasecurity.io/)
> See this presentation  https://www.slideshare.net/pumasecurity/secure-devops-a-pumas-tail  

[*open-source Visual Studio plugin for C#](https://security-code-scan.github.io/)  

[Microsoft DevSkim](https://github.com/Microsoft/DevSkim)  
[SonarLint](https://www.sonarlint.org/)


## Tools

Archerysec
> OPEN SOURCE ORCHESTRATION AND CORRELATION TOOL  
https://www.archerysec.com/  

OWASP Defect Dojo:
> Open Source DevSecOps
The leading application vulnerability management tool.
Built for both DevSecOps and traditional application security.  
(https://www.defectdojo.org/)

[ThreadFix](https://threadfix.it/)  
[Code Dx](https://codedx.com/)  

[Yelps pre-commit framework](https://pre-commit.com/)  Provides a set of hooks to run lint checking for different languages before code can be checked in.

[Overcommit](https://github.com/sds/overcommit): git hook manager that comes with several predefined checks. 

Carnigie Mellon University SEI on using this framework for security checks: https://docs.github.com/en/github/building-a-strong-community/creating-a-pull-request-template-for-your-repository

Automation tools for configuration management:

```bash
# Chef:
https://github.com/rubocop/rubocop
https://docs.chef.io/workstation/cookstyle/
https://github.com/chef/cookstyle/
https://blog.chef.io/goodbye-foodcritic/ *sunsetted Sept 2019

# Puppet:
https://puppet.com/blog/verifying-puppet-checking-syntax-and-writing-automated-tests
http://puppet-lint.com/https://github.com/floek/puppet-lint-security-plugins
https://github.com/tushartushar/Puppeteer

# Ansible:
https://github.com/ansible-community/ansible-lint
https://github.com/Checkmarx/kics

# CloudFormation:
https://github.com/stelligent/cfn_nag
https://github.com/Skyscanner/cfripper
https://github.com/aws-cloudformation/cfn-python-lint
https://github.com/aws-cloudformation/cloudformation-guard
https://github.com/bridgecrewio/checkov/
https://github.com/Checkmarx/kics

# Terraform:
https://github.com/bridgecrewio/checkov/
https://github.com/accurics/terrascan 
https://github.com/terraform-linters/tflint
https://github.com/tfsec/tfsec
https://github.com/wayfair/terrafirma
https://github.com/Checkmarx/kics
```  

**Java:**
- FindBugs: popular code quality checker for Java; includes basic security checking (http://findbugs.sourceforge.net/) 
- SpotBugs: current fork of FindBugs for Java 8 and later (https://github.com/spotbugs/spotbugs)  
- fb-contrib: additional bug checkers for FindBugs and SpotBugs (http://fb-contrib.sourceforge.net/)  
- Find Security Bugs: plugin to the FindBugs engine for security-specific checks (https://find-sec-bugs.github.io/)  
- PMD: another popular checker, for code quality and good coding practices (https://pmd.github.io/)  
- Checkstyle: coding best practices, clean code can be configured to support different coding standards (Oracle's or Google's), highlights bad/unsafe code, and will find some common coding bugs (https://github.com/checkstyle/checkstyle) 
- Error Prone: open-source of Google's custom static analysis error checkers for Java (https://github.com/google/error-prone)  
- Infer from Facebook: null pointers, resource leaks race conditions (https://fbinfer.com/)  
- SonarSource open-source (https://www.sonarsource.com/java/)  

**.NET/C#:**
- StyleCop (https://github.com/DotNetAnalyzers/StyleCopAnalyzers) enforces style and consistency rules
- Puma Scan (https://pumasecurity.io/) open-source Visual Studio/VS Code plugin, common vulnerability patterns, and taint analysis (commercial version available)
- Security Code Scan (https://security-code-scan.github.io/) open-source Visual Studio plugin built on top of the Roslyn compiler
- Roslynator (https://github.com/JosefPihrt/Roslynator/) collection of analyzers and refactorings for C# on top of the Roslyn compiler
- SonarSource open-source (https://www.sonarsource.com/csharp/)

**JavaScript:**
- JSHint: powerful static analysis checking for JavaScript (https://jshint.com/about/)
- JSLint: another static analysis checker, focusing on coding style (https://github.com/douglascrockford/JSLint)
- JSCS: JavaScript Code Style (https://github.com/jscs-dev/node-jscs)
- Closure Compiler: from Google, compiles JavaScript into better JavaScript; parses and analyzes code; removes dead code; rewrites and minimizes whats left; checks syntax, variable references, and types; and warns about common mistakes (https://developers.google.com/closure/compiler/)
- ESLint: powerful, rules-based code quality checker (https://eslint.org/)
- Flow (from Facebook) focuses on static type checking (https://flow.org/)
- NodeJsScan (https://github.com/ajinabraham/NodeJsScan) static security code scanner for Node.JS
- SonarSource open-source (https://www.sonarsource.com/js/)
  
**PHP:**
- Phan: comprehensive PHP static analysis in CI/CD by Rasmus Ledorf (PHP lead author) and others at Etsy. Developed in PHP 7, but can analyze code in any version of PHP, can be extended through plugins (https://github.com/phan/phan)
- Phan Taint Check: Security plugin for Phan (https://github.com/wikimedia/Phan-Taint-Check-Plugin)
- PHP CodeSniffer: Sanity and style checking (https://github.com/squizlabs/PHP_CodeSniffer)
- PHP Mess Detector: Looks for dead code, over-complex expressions, possible bugs (https://phpmd.org/)
- Progpilot: Extensible security analysis for PHP (https://github.com/designsecurity/progpilot)
- HHVM compiler for PHP and Hack from Facebook (https://hhvm.com/)
- RIPS: Commercial security checking for PHP, replaces abandoned open-source project (https://www.sonarsource.com/)
- Exakat: Real-time PHP code analyzer, includes some security checks (https://www.exakat.io/en/)
- PHP IDE analysis in IDE PhpStorm (https://www.jetbrains.com/phpstorm/)
- SonarSource open-source (https://www.sonarsource.com/php/)
  
**Ruby:**
- Brakeman security scanner was originally developed at Twitter (https://brakemanscanner.org/)
- Brakeman Pro is a commercial version of Brakeman that offers visualization and triage capabilities. It will eventually offer additional, deeper scanning capabilities (https://brakemanpro.com/)
- Dawnscanner: reviews Ruby/Rails code for security issues (https://github.com/thesp0nge/dawnscanner) 
- RuboCop: enforces Ruby Style guide (https://github.com/rubocop/rubocop)
- RubyCritic wraps other static analysis tools (e.g., Reek, Flay, and Flog) to help identify code smells (https://github.com/whitesmith/rubycritic)
- Railroader static analysis for Ruby on Rails (https://railroader.org/)
- SonarSource open-source (https://www.sonarsource.com/ruby/)
- RubyMine IDE (https://www.jetbrains.com/ruby/)

Python:
- Bandit is an open-source tool from OpenStack Security to find common security problems in Python code (https://github.com/PyCQA/bandit)
- Dlint helps ensure that Python code is secure (https://github.com/dlint-py/dlint)
- Googles Pytype (https://github.com/google/pytype)
- Pylint checks for bad coding practices and common errors (https://www.pylint.org/)
- PyCharm is a Python IDE from JetBrains, which includes static analysis checking capabilities. It is available in a free community and licensed professional edition (https://www.jetbrains.com/pycharm/)
- Pyre static analysis (type checking) from Facebook for Python 3 (https://pyre-check.org/)
- Pyright from Microsoft for large codebases (https://github.com/Microsoft/pyright)
- SonarSource open-source (https://www.sonarsource.com/python/)C/C++:
- Cppcheck https://github.com/danmar/cppcheck
- Clang https://clang-analyzer.llvm.org/
- OCLint https://oclint.org/
- Flawfinder https://dwheeler.com/flawfinder/
- Infer from Facebook https://fbinfer.com/
- SonarSource Commercial (https://www.sonarsource.com/c/)
  
**Objective C/Swift:**
- XCode has Analyze built-in for Objective-C. This is not available for Swift as of XCode 9.2 December 2017, although many of the checks performed by XCode Analyze are not necessary in Swift https://stackoverflow.com/questions/29326036/is-it-not-possible-to-use-analyze-with-swift 
- OCLint for Objective-C (http://oclint.org/)
- SwitfLint https://github.com/realm/SwiftLint
- Clang (Standalone or within Xcode) (https://clang-analyzer.llvm.org/)
- Infer: a static analysis tool from Facebook that looks for null pointer exceptions, resource leaks, and memory leaks (https://fbinfer.com/)
- Faux Pas (Commercial) analysis of Xcode (http://fauxpasapp.com/)
- SonarSource Commercial (https://www.sonarsource.com/swift/)

**Android**  In addition to common Java static analysis tools like Spotbugs, PMD, and error-prone, Android developers should consider these tools:
- IDEA and Android Studio. The IntelliJ IDEA IDE has built-in code analysis checking for Java and Android, and support for several plugins. Google's Android Studio is built on top of IntelliJ. https://developer.android.com/studio/intro/
- Android Lint checks for bugs, security, and performance (https://developer.android.com/studio/write/lint)
- Custom Android Lint Rules: template for writing custom lint rules (https://github.com/a11n/CustomLintRules)
- Infer: Static analysis tool from Facebook that looks for null pointer exceptions, resource leaks, and memory leaks (https://fbinfer.com/)
- Qark: Quick Android Review Kit looks for common security-related problems in source code or packaged APKs (https://github.com/linkedin/qark)

**Go** includes some basic static analysis checkers. Additional tools include:
- Vet: vets Go source, reports on suspicious constructs (focus on correctness) (https://golang.org/cmd/vet/)
- Lint: focuses on coding style (https://github.com/golang/lint)
- dingo-hunter: finds deadlocks (https://github.com/nickng/dingo-hunter)
- errcheck: checks for unhandled errors (https://github.com/kisielk/errcheck)
- Gosec: scans for common security weaknesses (https://github.com/securego/gosec)
- SafeSQL: checks SQL queries for SQL injections (https://github.com/stripe/safesql)
- Check: aligncheck, structcheck, varcheck (https://gitlab.com/opennota/check)
- SonarSource open-source (https://www.sonarsource.com/go/)See this list of Go static analysis tools: https://github.com/dominikh/go-toolsAlso, check out the following multi-language scanners:
- GitHub's CodeQL https://codeql.github.com/
- R2C's Semgrep: https://semgrep.dev/ 

## Commercial IDE plugins

[Checkmarx](https://www.checkmarx.com/plugins/)  
[Coverity plugins for Eclipse, IntelliJ, and Visual Studio](https://www.synopsys.com/content/dam/synopsys/sig-assets/datasheets/SAST-Coverity-datasheet.pdf)  
[SecureAssist](https://community.synopsys.com/s/article/SecureAssist-Overview)  
[Klocwork](https://www.perforce.com/solutions/static-analysis)  
[Microfocus Fortify plugins for Eclipse and Visual Studio ](https://marketplace.microfocus.com/fortify)  
[Veracode Greenlight](https://www.veracode.com/products/binary-static-analysis-sas)  


## Rapid Risk Assessment (RRA)  

- PayPal risk questionnaire for new apps/services  
- Mozilla Rapid Risk Assessment (RRA) model (30-minute review)
- Slack goSDL for questions to determine initial risk rating  
- template for RRA [here](template_RRA.md)


## Pre-Commit Hooks

- https://pre-commit.com/
- https://github.com/pre-commit/pre-commit
- https://github.com/sds/overcommit


## Pull Request Templates

- https://docs.gitlab.com/ee/user/project/description_templates.html#creating-merge-request-templates  
- https://help.github.com/en/github/building-a-strong-community/creating-a-pull-request-template-for-your-repository  
- https://docs.microsoft.com/en-us/azure/devops/repos/git/pull-request-templates?view=azure-devops  
- https://bitbucket.org/blog/save-time-with-default-pull-request-descriptions  
- https://mibexsoftware.atlassian.net/wiki/spaces/CRA/pages/4227082/Usage#Usage-Pullrequesttemplates  

# Links:

Examples of how to write your own checkers or plugins with popular SAST tools:
- https://access.redhat.com/blogs/766093/posts/1975913
- https://owasp.org/www-pdf-archive/ASDC12-Teaching_an_Old_Dog_New_Tricks_Securing_Development_with_PMD.pdf

