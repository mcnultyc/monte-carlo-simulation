# Compiling data
1. `pip install alpha_vantage`
2. `pip install pandas`
3. `python download_histories.sh -d`
    * This will use the alpha vantage api to download 20 years of historical data 
    for each company listed in [companies_list.txt](companies_list.txt). The file 
    created will be named stock_data.csv.

The format of the input file will have the following format, where each value under 
the tickers represents the percent change per day.

| date  | GOOGL | GE    | AAPL  | GS    | OIL  |
| ------|-------|-------|-------|-------|------|
| 2019-11-14 | -1.52  | -1.41  | 0.027 | -0.55 | 1.37 |
| 2019-11-13 | -0.14 | 0.98 | -0.99 | -0.18 | -1.95 |


# Homework 3
### Description: you will gain experience with the Spark computational model in AWS cloud datacenter.
### Grade: 10% + bonus up to 3% for implementing this simulator using M/R and comparing it to your Spark program on [AWS EMR](https://aws.amazon.com/emr).
#### You can obtain this Git repo using the command ```git clone git@bitbucket.org:cs441_fall2019/homework3.git```. You cannot push your code into this repo, otherwise, your grade for this homework will be ZERO!
#### Preliminaries are the same as in the previous homeworks.

## Functionality
Your homework assignment is to create a Spark program for parallel processing of the predictive engine for stock portfolio losses using Monte Carlo simulation in Spark. An example of a Monte Carlo simulation implementation is located in the [GitHub repository](https://github.com/vzlatkin/MonteCarloVarUsingRealData). You will follow the instructions, fix problems, and deploy the simulator at AWS EMR. In this homework you will use [Google Finance](https://support.google.com/docs/answer/3093281?hl=en&ref_topic=3105411) or some other web service to obtain historical securities information (i.e., stock prices). There are many guides and tutorials on the Internet how to configure a Apache Spark on YARN. Alternatively, for an additional 1% bonus you may deploy your simulator on the Google Computing Engine (GCE) platform that has a solution for Monte Carlo methods using [Google cloud Dataproc and Apache Spark](https://cloud.google.com/solutions/monte-carlo-methods-with-hadoop-spark).

The functionality of your Monte Carlo simulator includes the following. The input to your simulator is a randomly selected list of stocks, your total fund amount in USD, and a time period for which prices are recorded for these stocks at Google Finance or some other financial engine that contains this information. You will allocate your fund using some distribution criteria to purchase stocks at the beginning of the time period. As the simulation starts, your simulator records losses and gains as the simulation time goes by. The simulator makes decisions at some time points to sell stocks (e.g., to stop losses or because the gain  plateaued). If more fund money becomes available because of the gain from a stock sell or because of the new contributions to the fund, the simulator will select new stock ticker randomly and invest the money in it. As the simulation comes to the end, you will record the gains and losses. You can repeat the simulation as many times as you want.

To get you started, you may play around with many tutorials on implementing algorithms in Spark, specifically, I recommend a [Hortonworks tutorial on Spark](https://www.cloudera.com/tutorials/hands-on-tour-of-apache-spark-in-5-minutes.html). Of course, simply cloning and running the code will get you nowhere, so you will need to think how to implement your stock evalution simulation in Spark.

You will create and run your software application using [Apache Spark](https://spark.apache.org/), a framework for distributed processing of large data sets across multiple computers (or even on a single node) using iterative algorithms, such as PageRank. If your laptop/workstation is limited in its RAM, you can use [Cloudera QuickStart VM with the minimum req of RAM 4Gb](https://www.cloudera.com/downloads/quickstart_vms/5-12.html). Even though you can install and configure Spark on your computers, I recommend that you use a virtual machine (VM) of [Hortonworks Sandbox](http://hortonworks.com/products/sandbox/), a preconfigured Apache Spark installation with a comprehensive software stack. To run the VM, you can install vmWare or VirtualBox. As UIC students, you have access to free vmWare licenses, go to http://go.uic.edu/csvmware to obtain your free license. In some cases, I may have to provide your email addresses to a department administrator to enable your free VM academic licenses. Please notify me if you cannot register and gain access to the webstore.

As before, the steps for obtaining your free academic vmWare licenses are the following:
- Go to [Onthehub vmWare](http://go.uic.edu/csvmware).
- Click on the "sign in" link at the top.
- Click on "register".
- Select "An account has been created..." and continue with the registration.
- Make sure that you use the UIC email with which you are registered with the system.

Only UIC students who are registered for this course are eligible. If you are auditing the course, you need to contact the uic webstore directly. Alternatively, you can use [VirtualBox from Oracle Corp](https://www.virtualbox.org/).

As before, this homework script is written using a retroscripting technique, in which the homework outlines are generally and loosely drawn, and the individual students improvise to create the implementation that fits their refined objectives. In doing so, students are expected to stay within the basic requirements of the homework and they are free to experiments. Asking questions is important, so please ask away at Piazza!

You can complete this homework using Scala and __you will immensely enjoy__ the embedded XML or JSON processing facilities that come with Scala. You will use Simple Build Tools (SBT) for building the project and running automated tests. I recommend that you run the downloaded VM locally in vmWare or VirtualBox to develop and test your program before you move it to AWS.

Next, after creating and testing your map/reduce program locally, you will deploy it and run it on the Amazon Elastic MapReduce (EMR). You will produce a short movie that documents all steps of the deployment and execution of your program with your narration and you will upload this movie to [youtube](www.youtube.com) and you will submit a link to your movie as part of your submission in the README.md file. To produce a movie, you may use an academic version of [Camtasia](https://shop.techsmith.com/store/techsm/en_US/cat/categoryID.67158100) or some other cheap/free screen capture technology from the UIC webstore or an application for a movie capture of your choice. The captured web browser content should show your login name in the upper right corner of the AWS application and you should introduce yourself in the beginning of the movie speaking into the camera.

## Baseline Submission
Your baseline project submission should include your Apache Spark implementation of the Monte Carlo simulation, a conceptual explanation in the document or in the comments in the source code of how your iterative algoritnm works to solve the problem, and the documentation that describe the build and runtime process, to be considered for grading. Your project submission should include all your source code written in Scala as well as non-code artifacts (e.g., configuration files), your project should be buildable using the SBT, and your documentation must specify how you paritioned the data and what input/outputs are. Simply copying Java/Scala programs from examples at HGithub or other public open source repos and modifying them a bit will result in rejecting your submission.

## Piazza collaboration
You can post questions and replies, statements, comments, discussion, etc. on Piazza. For this homework, feel free to share your ideas, mistakes, code fragments, commands from scripts, and some of your technical solutions with the rest of the class, and you can ask and advise others using Piazza on where resources and sample programs can be found on the internet, how to resolve dependencies and configuration issues. When posting question and answers on Piazza, please select the appropriate folder, i.e., hw5 to ensure that all discussion threads can be easily located. Active participants and problem solvers will receive bonuses from the big brother :-) who is watching your exchanges on Piazza (i.e., your class instructor). However, *you must not describe your Monte Carlo design for Spark or specific details related how your construct your Spark deployment!*

## Git logistics
**This is an individual homework.** Separate repositories will be created for each of your homeworks and for the course project. You will fork this repository and your fork will be private, no one else besides you, the TA and your course instructor will have access to your fork. Please remember to grant a read access to your repository to your TA and your instructor. In future, for the team homeworks and the course project, you should grant the write access to your forkmates, but NOT for this homework. You can commit and push your code as many times as you want. Your code will not be visible and it should not be visible to other students (except for your forkmates for a team project, but not for this homework). When you push the code into the remote repo, your instructor and the TA will see your code in your separate private fork. Making your fork public, pushing your code into the main repo, or inviting other students to join your fork for an individual homework will result in losing your grade. For grading, only the latest push timed before the deadline will be considered. **If you push after the deadline, your grade for the homework will be zero**. For more information about using the Git and Bitbucket specifically, please use this [link as the starting point](https://confluence.atlassian.com/bitbucket/bitbucket-cloud-documentation-home-221448814.html). For those of you who struggle with the Git, I recommend a book by Ryan Hodson on Ry's Git Tutorial. The other book called Pro Git is written by Scott Chacon and Ben Straub and published by Apress and it is [freely available](https://git-scm.com/book/en/v2/). There are multiple videos on youtube that go into details of the Git organization and use.

Please follow this naming convention while submitting your work : "Firstname_Lastname_hw2" without quotes, where you specify your first and last names **exactly as you are registered with the University system**, so that we can easily recognize your submission. I repeat, make sure that you will give both your TA and the course instructor the read access to your *private forked repository*.

## Discussions and submission
You can post questions and replies, statements, comments, discussion, etc. on Piazza. Remember that you cannot share your code and your solutions privately, but you can ask and advise others using Piazza and StackOverflow or some other developer networks where resources and sample programs can be found on the Internet, how to resolve dependencies and configuration issues. Yet, your implementation should be your own and you cannot share it. Alternatively, you cannot copy and paste someone else's implementation and put your name on it. Your submissions will be checked for plagiarism. **Copying code from your classmates or from some sites on the Internet will result in severe academic penalties up to the termination of your enrollment in the University**. When posting question and answers on Piazza, please select the appropriate folder, i.e., hw1 to ensure that all discussion threads can be easily located.


## Submission deadline and logistics
Sunday, November 17 at 11PM CST via the bitbucket repository. Your submission will include the code for the Spark stock simulation program, your documentation with instructions and detailed explanations on how to assemble and deploy your Spark Monte Carlo stock simulation along with the results of its run (i.e, which stock package to invest into), and a document that explains how you designed and implemented the program, and what the limitations of your implementation are. Again, do not forget, please make sure that you will give both your TA and your instructor the read access to your private forked repository. Your name should be shown in your README.md file and other documents. Your code should compile and run from the command line using the commands ```sbt clean compile test``` and ```sbt clean compile run```. Also, you project should be IntelliJ friendly, i.e., your graders should be able to import your code into IntelliJ and run from there. Use .gitignore to exlude files that should not be pushed into the repo.


## Evaluation criteria
- the maximum grade for this homework is 10% with the bonus up to 3% for doing the AWS EMR part. Points are subtracted from this maximum grade: for example, saying that 2% is lost if some requirement is not completed means that the resulting grade will be 10%-2% => 8%; if the core homework functionality does not work, no bonus points will be given;
- the code does not work in that it does not produce a correct output or crashes: up to 10% lost;
- having less than five unit and/or integration tests that test the main functionality: up to 7% lost;
- missing comments and explanations from the program: up to 6% lost;
- logging is not used in the program: up to 8% lost;
- hardcoding the input values in the source code instead of using the suggested configuration libraries: up to 9% lost;
- no instructions in README.md on how to install and run your program: up to 10% lost;
- the documentation exists but it is insufficient to understand how you assembled and deployed all components of the cloud: up to 5% lost;
- the minimum grade for this homework cannot be less than zero.

That's it, folks!