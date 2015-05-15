(Nothing here, but this seems like fun, so I created a repo.)

Consider the following common idiom:

    class Foo(object):

        def __init__(self):
            self._attr = None

        @property
        def attr(self):
            if self._attr is None or we_want_a_new_one():
                attr = calculate_attr()
                self._attr = attr
            return self._attr

        @attr.setter
        def attr(self, value):
            attr = calculate_attr()
            self._attr = attr

Why should it be necessary to do this by hand each and every time? Instead, let's

    class Foo(object, ExpensiveAttrs):

        def __init__(self):

            self.attr = self.create_expensive_attr(
                setter=calculate_attr,
                expiry_condition=we_want_a_new_one,
            )

