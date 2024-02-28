# aws-certified-solutions-architect-cantrill-notes
My personal notes from Adrian Cantrill's course for AWS Certified Solutions Architect - Associate (SAA-C03).

Results: Passed on the first attempt. 

140 hours of study, May 1 - August 10 Mon-Fri

Tools:
- Cantrill's SAA-C03 course (1.5x speed, pausing to take notes)
- Tutorials Dojo SAA-C03 practice exam collection
- AWS docs
- Flash cards on phone while vacationing (Quizlet app free version, found collections made by other users)

Exam: August 11
Studied roughly 3 hours a day usually using the Pomodoro technique (25min study, 5min break, repeat). Basically spent 95% of the time just going through Cantrill's course and taking notes. I would go in to Tutorials Dojo to reinforce the topic I learned with quizzes and reviews. And Googling often when I didn't understand concepts or how different services connected. For the last 5 days after I finished Cantrill's course, I focused on the Tutorials Dojo full practice exams, all timed. I would then review what I answered incorrectly and then retake the same exam to get a 95%+. I did each exam twice in a row and completed two new exams a day. During a vacation during my study period, I brought some flashcards on my phone found on Quizlet to just keep the content close in mind, but not study heavily during the break. I burned out a few times and took a 3 day weekend here and there, as well.

I had to reschedule the exam twice after realizing I did not allot enough time to get through all the Cantrill material (I honestly ended up skipping some demos towards the end just to get through the content).

In terms of the actual exam, I found that the content and questions were overall pretty difficult and not exactly what I practiced on Tutorials Dojo. However, hammering out quizzes/exams over and over gave me the ability to break down the questions and logic out the answers drawing from what I learned studying. I think it was very valuable that I reinforced Cantrill learnings frequently with quizzes and Google research related to the studied topic. I never had issues with the exam time running out, my issue was really just  mainly absorbing this massive amount of info and actually being able to understand each component and connect the dots.

Overall, the content and certification exam was difficult, but entirely doable on the first attempt if you use your resources and stay consistent. Good luck!
___
What's Next? It was recommended to me (by a friend who works professionally in AWS) that I complete the Cloud Resume Challenge which has been extremely valuable so far. I am a self-taught developer with 2 years of professional Web Dev experience and the CRC challenge is helping me bridge the gap from AWS study to job-readiness. I'll be able to share this project and its results with recruiters/hiring managers to display my abilities

# Basic Account Setup 
1. create account and root user
2. add alt contact info
3. billing notifications, create free-tier budget (skip MFA and security), "CRC Zero-Spend Budget"
4. create IAM admin 
- create alias for sign in
5. sign in with crc-admin
6. create access keys
-public
-secret
7. configure CLI (command prompt) ``aws configure --profile crc-admin
