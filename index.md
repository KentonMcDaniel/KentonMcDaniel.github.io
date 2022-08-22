Kenton McDaniel

1.	What is application security and how does it differ from platform security? 

    	This question is open to a broad interpretation and is a thought exercise to see how a candidate handles the differentiation. I consider application security to be the view of how the application is secured from the first architectural diagram and after it is deployed to a production workload. Platform security is application security but additionally making sure that the platform is configured correctly to support your security objectives for the applications and your business.
      
2.	How do you identify weaknesses in application architecture?

    This is another thought exercise. I generally try to get an idea of how the data is going to be used and flow through the application. Then I identify points at which the architecture can be taken advantage of or compromised. I try to pay attention to current technology so that I am aware of performance impacts of architectural decisions as well. The final piece is understanding how the data will be used to make sure I understand business logic errors.
    
3.	How do you audit encryption implementations? 

	I compare against known encryption standards. If someone is trying to roll their own crypto in this day and age I point them directly to industry standards that have been reviewed by someone much smarter than me. I also look at common implementations to make sure we are using the standards correctly.
  
4.	What is privilege escalation? Tell me about your last successful privesc? 

	Privilege escalation is the process of gaining more privileges in a system than you should be able to get. The last successful privesc I performed was a dll hijack of a windows service that was loading a binary from a location with global write privileges assigned to it.
  
5.	Describe in as much detail as possible how to provision an IAM account in AWS.

	For this question my answer would be: I would refer to AWS best practices guides and company documentation for how to provision an IAM user in accordance with the policies in place.
  
6.	What is the difference between SAST, DAST, SCA, IAST?

	SAST: Static Application Security Testing: Scanning source code, binaries, configs, and other artifacts for vulnerabilities that are known or patterns that show vulnerability.
	DAST: Dynamic Application Security Testing: Performing testing on a running version of an application/service/piece of running code checking for vulnerabilities. This can and should be automated.
	SCA: Software Composition Analysis: Checking your software projects for vulnerabilities in third parties and other imported pieces of code.
	IAST: Interactive Application  Security Testing: Performing interactive testing of the application/service/running code checking for vulnerabilities.
	How can you implement SAST, DAST, and SCA into a CI/CD pipeline? 
	You can implement these controls at every step of a mature pipeline. It depends on how the pipeline is architected and how you want to instrument. Recommend not gating commits at the outset until your teams are comfortable with getting failed pushes due to security issues.
  
8.	Explain container escapes to me. 

	The idea is that you escape a running container into the host OS. You leverage a vulnerability to execute code, write files, or otherwise gain access to sensitive data or processes on the host OS that allow you to do things beyond the constraint of the container.
  
9.	What tasks make you lose track of time? 

	This is a thought exercise to see if the candidate can identify tasks that draw their full attention. This is different for everyone and often changes over time. For me: I lose track of time when I have a small proof of concept exploit that I want to take further. I also lose track of time when doing IR when there is an IOC. I also lose track of time writing policies that are meaningful and impactful. I also lose track of time when playing some card and board games with my family.
  
10.	Review this application architecture diagram and tell me how you would attack the application: 

	The diagram in question is incredibly simplistic. I’ll start from the top boxes and work my way down: User auth service: I would look at the JWT and look for common vulnerabilities and for common mistakes with provisioning JWTs. Load it up in jwt.io and start inspecting. The fact that the JWT allows for NULL tells me it would be completely broken. I’d check for ALG:NONE and other things that would let me forge my own JWT. CRUD screens only doing client side validation tells me that I can likely bypass these checks using a proxy (BurpSuite) and potentially exploit vulnerable components. Orgs being identified via a query string identifier would have me looking for IDOR off the bat. There are many more things to look at but these are the ones that stand out and that I wrote the diagram to evoke.
  
11.	At which points in that application server architecture will load become prohibitive?

	There’s a single Load Balancer. 3 application servers might not be sufficient. I don’t state whether or not the Ubuntu webservers are containers, VMs, or physical machines. The webservers might buckle under load and not be able perform properly depending on the resources provisioned to them.
  
12.	Describe how you would change the architecture you see in both the application level and the server level? 

	This is something I would indicate is a much more broad discussion that cannot happen during an interview but I would focus on this: Make sure we are containerizing the workload and depending on hosting model make sure we leverage native cloud services where possible.
  
13.	What is CORS? 

	Cross Origin Resource Sharing.
  
14.	Describe threat modeling. 

	Coming to a consensus about the risk profile, attack surfaces, and acceptable risk for a given project.
  
15.	How would you reverse engineer a binary knowing nothing about it beforehand?

	Set it up inside of a sandbox environment and watch the behavior. Strings the binary and check for information. Open it up in r2/IDA/Ghidra/dnSPY depending on what it is and start looking into what it is.
  
16.	What is the most recent security related subject you’ve been learning about or would like to learn more about?
 
	I have been learning about Cloud native service offerings that can replace expensive vendor tooling. Often times we don’t need the full suite of what expensive vendors offer to satisfy what kind of protection our workload needs.
  
17.	How comfortable are you with offering advice on more complex vulnerable code paths that other engineers are unsure about? 

	Depending on the language and implementation I waver between comfortable and extremely comfortable.
