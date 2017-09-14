<h1> PyPermissions </h1>

PyPermissions is one cool repo. Strict and firm, but easy-going when needed. He doesn't always let you
do what you want, but when he does, you must always ask for **permission**. PyPermissions may not be considered
your *conventional* repo, but its *your* PyPermissions and you love him all the same.

PyDad extends class methods to give methods various permissions (inside class, outside class,
super class, sub class, etc.)

```python
    class Foo(object):
        def __init__(self):
            pass

        def secret_private_method(self);

        @add_permits("1")
        def foo1(self):
            self.r1()
            self.foo2()

        @add_permits("2")
        def foo2(self):
            """ Can only be called if its called from foo1 """
            assert self.get_permits() == ["1", "2"]
            self.r1() # ok, if called from foo1
            self.r2() # ok
            foo3()

        @add_permits("3")
        def foo3(self):
            assert self.get_permits() == ["1", "2", "3"]
            try:
                self.r123() # only ok if called from a foo1, foo2 chain
            except PermissionError as e:
                print("r123 must be called from methods with permissions 1, 2 and 3"!)
                raise e

        @require_permits("1")
        def r1(self):
            pass

        @require_permits("2")
        def r2(self):
            pass

        @require_permits("1", "2", "3", method="all", callback=None)
        def r123(self):
            pass
```
