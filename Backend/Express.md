__Problem 1__: I was trying to access the `id` of an object through the `req.params` and was getting the `id` but within an _Object_ 
![[Pasted image 20250321201825.png]]
__Solution__: This happened because in my `applicant.ruotes.js` file, the route for applying to the job through `jobId` was defined as such
![[Pasted image 20250321202007.png]]
`/:jobId/apply` is having looking for `id` in the certain pattern and if express finds it than add to the field as `jobId`. 