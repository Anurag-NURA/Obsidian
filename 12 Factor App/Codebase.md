	"One codebase tracked in revision control, many deploys"

It is to have only one codebase. Everyone in the team should work only in codebase so that conflict between different versions of codebase doesn't arise. [[Git]] helps the developers to achieve this goal and make codebase available to everyone and let them know of any changes made. GitLab and GitBucket is another alternative of GitHub. 

Consider you have a web application, In the future we may have order processing service or a delivery service. Now we no longer have a single system, we have a [[Distributed System ]]. 
![[Pasted image 20240915084512.png]]


==**☝ Multiple app sharing the same code is a violation of twelve-factor app.**== Every service should be separated into its own individual code bases. 
![[Pasted image 20240915084533.png]]


The codebase is the same across all deploys, although different versions may be active in each deploy. For example, a developer has some commits not yet deployed to staging; staging has some commits not yet deployed to production. But they all share the same codebase, thus making them identifiable as different deploys of the same app.
![[Pasted image 20240915084723.png]]
