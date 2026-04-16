_A way to process and transform documents in stages_. In mongoDB, we can perform join operations like in SQL to see the results of table referencing each other. 

We use `$lookup` specifically for to perform `Left Join` on tables. 

Let's take example from our actual project

__Applicant Schema__
![[Pasted image 20250323151200.png]]

__Jobs Schema__
![[Pasted image 20250323151236.png]]

__User Schema__
![[Pasted image 20250323151439.png]]

As you can see in `Applicant` schema, we referenced the `User` schema for users who will be applying for a specific `Job` and then that user's and job's `id` will be stored in `Applicant` collection as a new applicant. But now let's say we want to check all the applicants for a particular job then the query to perform for looking that data will be like a `Left Join Operation`

```json
db.jobs.aggregate([
	{
		$lookup:{
				from: "applicants",
				localField: "_id",
				foreignField: "job",
				as: "results"
			}
		}
	}
]).pretty()
```

This will take all the values from left collections i.e., from `jobs`, and will join with `applicants` collections on the basis of `localField` of `_id` and `foreignField` of `job`. 

Result will be like this: 
![[Pasted image 20250323152605.png]]