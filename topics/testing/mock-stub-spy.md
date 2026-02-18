# Mock, Stub, Spy

__Mock__ = fake object replacing the real one with dummy data. Used to validate the program flow in isolation because the mock fully substitutes the real code.

__Stub__ = more specific mock object returning prepared data, often hardcoded. Used to validate different conditions.

__Spy__ = partial mock that keeps the real object but replaces a subset of its methods. Used to record how the real production code is used without interfering with it.
