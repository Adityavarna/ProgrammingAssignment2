# ProgrammingAssignment2
> ## The <<- operator which can be used to assign a value to an object in an environment that is different from the current    ##environment. Below are two functions that are used to create a special object that stores a numeric vector and caches its   ##inverse.
> 
> ## The first function, makeCacheMatrix creates a special "vector", which is really a list containing a function to set the   ##values of the matrix,get the values of the matrix,set the values of the inverse,get the values of the inverse
> m <- c(2,3,4,5)
> mat=matrix(m,nrow=2)
> makeCacheMatrix <- function(x = numeric()) {
+         m <- c(2,3,4,5)
+         mat=matrix(m,nrow=2)
+         set <- function(y) {
+                 x <<- y
+                 m <<- c(2,3,4,5)
+         }
+         get <- function() x
+         setsolve <- function(solve) mat <<- solve
+         getsolve <- function() mat
+         list(set = set, get = get,
+              setsolve = setsolve,
+              getsolve = getsolve)
+ }
> ##The following function calculates the inverse of the matrix created with the above function. However, it first checks to   ##see if the inverse has already been calculated. If so, it gets the mean from the cache and skips 
  ##the computation.Otherwise, it calculates the inverse of the data and sets the value of the inverse in the cache 
  ##via the setsolve function. 
> cacheSolve <- function(x, ...) {
+         mat <- x$getsolve()
+         if(!is.null(mat)) {
+                 message("getting cached data")
+                 return(mat)
+         }
+         data <- x$get()
+         mat <- solve(data, ...)
+         x$setsolve(mat)
+         m
+ }
##SampleOutput
##Solve function executes the inverse of the matrix
> solve(mat)
     [,1] [,2]
[1,] -2.5    2
[2,]  1.5   -1
> 
