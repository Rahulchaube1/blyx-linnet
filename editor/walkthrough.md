## Bridge short pauses in a speech-activity trace

Returns [first active millisecond, exclusive active end, segment count, retained active-or-bridged milliseconds]. A silent trace returns [-1,-1,0,0]. Invalid arguments and nonfinite results return an empty vector.

1. Open an empty file named `linnet-demo.blyx`.
2. Type `blyx-linnet-demo` and select **Linnet — runnable example**. You can also use **Snippets: Fill File with Snippet**.
3. Choose **Blyx: Run File** from the command palette. Change an argument near the end of `fn main()` to try another input.

Expected output

```text
10
70
2
40
```

[Work through the example in the browser](https://www.blyx-lang.space/play?example=package-linnet)
