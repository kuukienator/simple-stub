# simple-stub

To simply make stubs out of simple javascript objects. Use this stubs for testing in your favorite testing setup.

## How to use

To create a stub object, create a object and call `.createStub()` with it as argument.

```js
    const obj = {
      f: a => a + 5,
    };

    const stubObj = simpleStub.createStub(obj);
```

If you now call `stubObj.f(1)` it will behave like `obj.f(1)` and return `6`. The stub object will also save an array with "Call-Objects" for each function call which looks like this:

```json
[{
  "args": [1],
  "err": undefined,
  "result": 6
}]
```

These "Call-Objects" can be found under the path `stubObj.calls.{function}`.

After you made your calls you can use this data to make your assertions.

```js
  it('calls the function 3 times with 1 2 and 3', () => {
    const obj = {
      f: a => a + 5,
    };

    const stubObj = simpleStub.createStub(obj);

    stubObj.f(1);
    stubObj.f(2);
    stubObj.f(3);

    expect(stubObj.calls.f.length).to.equal(3);
    expect(stubObj.calls.f[0].args[0]).to.equal(1);
    expect(stubObj.calls.f[0].result).to.equal(6);
    expect(stubObj.calls.f[1].args[0]).to.equal(2);
    expect(stubObj.calls.f[1].result).to.equal(7);
    expect(stubObj.calls.f[2].args[0]).to.equal(3);
    expect(stubObj.calls.f[2].result).to.equal(8);
  });
```

That's it.