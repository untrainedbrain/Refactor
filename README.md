# Refactor
Impossible to Refactor Code that has been Refactored under Vanderdecken's Seven Rules
This is an effort to solve the problem of writing poor software code. 

[This is a work in progress, don’t go all ape shit about so rule you don’t like or don’t understand just yet.]

The examples are written to be generic, please do not complain the syntax used.
This is a work in progress, don’t go all ape shit about so rule you don’t like or don’t understand just yet.

While there are many schools of how to write software correctly not many of them ever reach developers intact. Developers struggle without leadership and definite rules that can be applied to their code.

I present Vanderdecken’s Rules

No functions or methods or blocks with more than seven statements
What are not statements
  Comments
  local variable initialization
  static variable initialization
  block brackets
  the single return point

All functions or methods must only have a single return or exit point which is the last item in the block 

All functions that return a value must declare, initialize, assign and return only that one variable

Do not hide code in #defines
  create an inline or closure or a function

Do not hide values in #defines
  Use an enumeration

Do not optimize code
  Leave optimization to the compilers and languages
  Moore’s Law means that by the time you finish you 20% optimization the computers will be 100% faster

Elegant code works better
  But don’t try to nuance to the point of being unreadable garbage

All logic blocks and all loop block require brackets (if supported by the language 

All if blocks need an else block

	func foo( x )
	{
	int ret = ?

	if ( x == 0 )
		ret = true
	else	
		if ( x == 1 )
			ret = false
	return( ret )
}

So what if x == -1 ? the return could be undefined
	
	func foo( x )
	{
	int ret = undefined
	if ( x == 0 )
	{	
		ret = true
	}else	
		if ( x == 1 )
		{
			ret = false
		}
		else
		{
			ret = 2
		}
}
	return( ret )


Called functions cannot crash on error
  They need to fail gracefully

All class methods must leave the class instance in a stable state
  If the method is going to fail, then it must make sure not to leave the class instance in an unstable state.
  Do not modify class members until the outcome is known and safe to return.
    Don’t do this
    Do not set class methods to new values until the computations are done
      class method foo( X )
      {
          self.y = 15
        self.w = X
        failure
      }
    Think about how rollbacks work. Do not trash the class before doing work that might fail. Back up the class if needed.
    Do the work, get a valid result, then, and only then modify the class or reset it to the condition you found it

For the love of God, do not use a sleep() to fix a multi-threaded problem

All blocks are required to have brackets if the language allows
      The problem is this
        if ( x == 1 )
          y = x
        else
          y = -x

        return

      What usually happens is another line of code is sneaked in

        if ( x == 1 )
          y = x
        else
          y = -x
          w = x*y

        return
      Now, instead of only doing w = x * y if x != 1, w = x*y happens every time.
