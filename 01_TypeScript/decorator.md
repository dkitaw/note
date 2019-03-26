```ts
import * as React from "react";
import "./App.css";
function log(
  target: object,
  propertyKey: string,
  descriptor: TypedPropertyDescriptor<any>
): any {
  const originalMethod = descriptor.value; // save a reference to the original method

  // NOTE: Do not use arrow syntax here. Use a function expression in
  // order to use the correct value of `this` in this method (see notes below)
  descriptor.value = function(...args: any[]) {
    // pre
    // console.log("The method args are: " + JSON.stringify(args));
    alert(JSON.stringify("The method args are: " + JSON.stringify(args)));
    // run and store result
    const result = originalMethod.apply(this, args);
    // post
    // console.log("The return value is: " + result);
    alert(JSON.stringify("The return value is: " + result));
    // return the result of the original method (or modify it before returning)
    return result;
  };

  return descriptor;
}
class App extends React.Component {
  public val = this.myMethod("xxx");
  @log
  public myMethod(arg: string) {
    return "Message -- " + arg;
    // alert(JSON.stringify("Message -- " + arg);
  }
  public render() {
    return <div className="App">App {this.val} </div>;
  }
}
// console.log(App);
export default App;

```
