## Programming Assignment 2: Lexical Scoping
Assignment: Caching the Inverse of a Matrix
Part of R Programming course, by Coursera (https://www.coursera.org/learn/r-programming/home/info)

##Creating the cache
###makeCacheMatrix
Starting from a new matrix or having it passed to the function, 'makeCacheMatrix' will return a list with four functions.
This four functions enables the cache maintenance. Two of them are meant to be used internally, and two externally.
The external functions, setsolve and getsolve will respectivelly set and get the data to be managed

<!-- -->

    makeCacheMatrix <- function(x = matrix()) {
        m <- NULL
        set <- function(y) {
            x <<- y
            m <<- NULL
        }
        
        get <- function() x
        
        setsolve <- function(val) m <<- val
        
        getsolve <- function() m
        
        list(set = set, get = get,
            setsolve = setsolve,
            getsolve = getsolve)
    }

### Using cache to increase performance
Given an previously created cache (see makeCacheMatrix above), cacheSolve will return an inverted given matrix.
Only the last cached object will be returned. If the matrix changes, makeCacheMatrix must be called again

    cacheSolve <- function(x, ...) {
        m <- x$getsolve()
        if(!is.null(m)) {
            message("getting cached data")
            return(m)
        }
        m <- solve(...)
        x$setsolve(m)
        m
    }
    
### Author
Marcos Braga Choma, 2017-06-10