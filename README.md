# Run Python Selenium Tests with Jenkins on TestMu AI (Formerly LambdaTest)

[![TestMu AI](https://img.shields.io/badge/TestMu%20AI-Formerly%20LambdaTest-blue)](https://www.testmuai.com/)
[![Selenium](https://img.shields.io/badge/Selenium-Testing-green)](https://www.testmuai.com/)

Jenkins Pipeline is also referred to as "Pipeline" offers a suite of plugins to help integrate your continuous delivery pipeline into Jenkins. Jenkins Pipeline does so with the help of Pipeline DSL(Domain Specific Language) syntax that facilitates easy modelling of even the most complex delivery pipeline. 

You can easily create a Jenkins pipeline for Python-selenium automation tests on TestMu AI (Formerly LambdaTest) using the following steps. You can refer to sample test repo [here](https://github.com/LambdaTest/python-selenium-sample).


## Getting Started with TestMu AI (Formerly LambdaTest)

TestMu AI (Formerly LambdaTest) is an AI-native, multi-agent quality engineering platform for running Selenium, Playwright, Cypress, Appium, and more at scale across 3000+ real browsers and OS combinations.

[Sign up for free](https://accounts.testmuai.com/register) · [Docs](https://www.testmuai.com/support/docs/)

## Prerequisites For Configuring Jenkins Pipeline With TestMu AI (Formerly LambdaTest)

1.  Jenkins 2.X or greater version.
2.  A Jenkins User with root access.
3.  Ensure you have the Pipeline plugin, although, it is displayed under the "suggested plugins" during the post-installation setup of Jenkins.
4.  **TestMu AI (Formerly LambdaTest) Authentication Credentials**
Be aware of your TestMu AI (Formerly LambdaTest) authentication credentials i.e. your TestMu AI (Formerly LambdaTest) username, access key and HubURL. You need to set them up as your environment variables. You can retrieve them from your  **TestMu AI (Formerly LambdaTest) automation dashboard**  by clicking on the key icon near the help button.

-   For Linux/Mac:
    
    ```
    $ export LT_USERNAME= {YOUR_LAMBDATEST_USERNAME}$ export LT_ACCESS_KEY= {YOUR_LAMBDATEST_ACCESS_KEY}
    ```
    
-   For Windows:
    
    ```
    $ set LT_USERNAME= {YOUR_LAMBDATEST_USERNAME}$ set LT_ACCESS_KEY= {YOUR_LAMBDATEST_ACCESS_KEY}
    ```
## Setting Up Jenkins Pipeline

Find the code for setting up a pipeline for the sample Python-selenium repo.
```bash
pipline 
{
    withEnv(["LT_USERNAME=Your LambdaTest UserName",
    "LT_ACCESS_KEY=Your LambdaTest Access Key",
    "LT_TUNNEL=true"]){

    echo env.LT_USERNAME
    echo env.LT_ACCESS_KEY 

    stages{
        stage('setup') { 

            // Get some code from a GitHub repository
            try{
            git 'https://github.com/LambdaTest/python-selenium-sample'

            //Download Tunnel Binary
            sh "wget https://s3.amazonaws.com/lambda-tunnel/LT_Linux.zip"

            //Required if unzip is not installed
            sh 'sudo apt-get install --no-act unzip'
            sh 'unzip -o LT_Linux.zip'

            //Starting Tunnel Process 
            sh "./LT -user ${env.LT_USERNAME} -key ${env.LT_ACCESS_KEY} &"
            sh  "rm -rf LT_Linux.zip"
            }
            catch (err){
            echo err
        }

        }
        stage('build') {
            // Installing Dependencies
            sh 'pip install -r requirements.txt'
            }

        stage('test') {
                try{
                sh 'python lambdatest.py'
                }
                catch (err){
                echo err
                }  
        }
        stage('end') {  
            echo "Success" 
            }
        }
    }
}

```
You can now add this script when creating the pipeline by using the following steps:

1. Create new pipleline
2. Scroll down to Advanced Project Options.
3.  Paste the Code in the code pane or fetch it via SCM & hit the **Save** button.

**Note:**  To run on the tunnel, Either you can use LT_TUNNEL Environment variable to set the tunnelling capability or you can pass in the code. Instructions on the tunnel are are available in the sample repo readme.

## TestMu AI (Formerly LambdaTest) Community

Connect with testers and developers in the [TestMu AI Community](https://community.testmuai.com/). Ask questions, share what you are building, and discuss best practices in test automation and DevOps.

## TestMu AI (Formerly LambdaTest) Certifications

Earn free [TestMu AI Certifications](https://www.testmuai.com/certifications/) for testers, developers, and QA engineers. Validate your skills in Selenium, Cypress, Playwright, Appium, Espresso and more. Industry-recognized, shareable on LinkedIn, and built by practitioners, not marketers.

## Learning Resources by TestMu AI (Formerly LambdaTest)

Learn modern testing through tutorials, guides, videos, and weekly updates:

* [TestMu AI Blog](https://www.testmuai.com/blog/)
* [TestMu AI Learning Hub](https://www.testmuai.com/learning-hub/)
* [TestMu AI on YouTube](https://www.youtube.com/@TestMuAI)
* [TestMu AI Newsletter](https://www.testmuai.com/newsletter/)

## LambdaTest is Now TestMu AI

On **January 12, 2026**, [LambdaTest evolved to TestMu AI](https://www.testmuai.com/lambdatest-is-now-testmuai/), the world's first fully autonomous **Agentic AI Quality Engineering Platform**.

Same team. Same infrastructure. Same customer accounts. All existing LambdaTest logins, scripts, capabilities, and integrations continue to work without change.

🏠 Find the new home for [LambdaTest](https://www.testmuai.com).

### How LambdaTest Evolved into TestMu AI

In 2017, we launched LambdaTest with a simple mission: make testing fast, reliable, and accessible. As LambdaTest grew, we expanded into Test Intelligence, Visual Regression Testing, Accessibility Testing, API Testing, and Performance Testing, covering the full depth of the testing lifecycle.

As software development entered the AI era, testing had to evolve, too. We rebuilt the architecture to be AI-native from the ground up, with autonomous agents that **plan, author, execute, analyze, and optimize tests** while keeping humans in the loop. The platform integrates with your repos, CI, IDEs, and terminals, continuously learning from every code change and development signal.

That evolution earned a new name: **TestMu AI**, built for an AI-first future of quality engineering. TestMu is not a new name for us. It is the name of our annual community conference, which has brought together 100,000+ quality engineers to discuss how AI would reshape testing, long before that became an industry norm.

What started as a high-performance cloud testing platform has transformed into an AI-native, multi-agent system powering a connected, end-to-end quality layer. That evolution defined a new identity: LambdaTest evolved into TestMu AI, built for an AI-first future of quality engineering.

## Support

Got a question? Email [support@testmuai.com](mailto:support@testmuai.com) or chat with us 24x7 from our chat portal.
