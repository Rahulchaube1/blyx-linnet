<img src="assets/logo.png" width="112" height="112" alt="Linnet logo">

# Linnet

Summarize speech-activity intervals from a precomputed frame-level envelope. This Blyx workflow framework is part of the vision, audio and speech collection.

A brief pause inside an utterance can split a segment. Accept a caller-selected gap and preserve the original time axis. [librosa, splitting a signal into active intervals](https://librosa.org/doc/0.11.0/generated/librosa.effects.split.html)

## Install and run

Install [Blyx 0.2.1](https://www.blyx-lang.space/download) with a Rust toolchain and host linker for native builds.

```sh
git clone --depth 1 --branch v0.1.1 https://github.com/Rahulchaube1/blyx-linnet.git
cd blyx-linnet
blyxc native-run example.blyx
blyxc native-run tests.blyx
```

[Run the editable browser example](https://www.blyx-lang.space/play?example=package-linnet) · [Package page](https://www.blyx-lang.space/packages/linnet) · [Handbook](https://doc.blyx-lang.space/guide/linnet)

## Import the module

Run this in the directory containing your application's entry file.

```sh
git clone --depth 1 --branch v0.1.1 https://github.com/Rahulchaube1/blyx-linnet.git vendor/linnet
```

```blyx
use vendor::linnet::linnet;

fn main() {
    let levels = [0, 3, 0, 3, 0, 0, 3];
    let threshold = 1.0;
    let gap = 1.0;
    let frame_ms = 10.0;
    let result = linnet_segment(levels, threshold, gap, frame_ms);
    if len(result) == 0 { println!("invalid"); return; }
    let mut i = 0;
    while i < len(result) {
        println!(at(result, i));
        i += 1;
    }
}
```

Expected output

```text
10
70
2
40
```

## API

`linnet_segment(levels, threshold, gap, frame_ms)`

Returns [first active millisecond, exclusive active end, segment count, retained active-or-bridged milliseconds]. A silent trace returns [-1,-1,0,0]. Invalid arguments and nonfinite results return an empty vector. Integers carried in numeric vectors use the exact range from −(2^53−1) to 2^53−1.

| Argument | Domain |
| --- | --- |
| levels | Vector of values, each a nonnegative finite number |
| threshold | A nonnegative finite number |
| gap | A nonnegative exact integer |
| frame_ms | A positive finite number |

## Run the command-line project

Run the example with your own numbers. Vector arguments accept up to 16 comma-separated entries; use `[]` for an empty vector. The imported API accepts longer vectors. Invalid arguments return a nonzero exit status.

```sh
blyxc native-run project.blyx -- "0,3,0,3,0,0,3" 1 1 10
```

## Libraries

- [ActivitySpan](https://github.com/Rahulchaube1/blyx-activityspan/tree/v0.1.1) — Locate active frames in a sequence of nonnegative signal levels.
- [GapHold](https://github.com/Rahulchaube1/blyx-gaphold/tree/v0.1.1) — Count activity segments while bridging short internal silences.

This release includes identical copies of both library modules so a tagged clone can build offline.

## Verification and contributions

The regression suite in [tests.blyx](tests.blyx) checks the example, boundary cases and invalid inputs. Include a short reproducer and your compiler version in [an issue](https://github.com/Rahulchaube1/blyx-linnet/issues). The source is dual-licensed under [MIT](LICENSE-MIT) or [Apache-2.0](LICENSE-APACHE). The package artwork uses [Lucide icons](https://lucide.dev/license); see [artwork notices](assets/NOTICE.txt).

## Connect with Rahul Chaube

[Portfolio](https://www.rahulchaube1.com/) · [GitHub](https://github.com/Rahulchaube1) · [LinkedIn](https://www.linkedin.com/in/rahulchaube1) · [Hugging Face](https://huggingface.co/oncody) · [X](https://x.com/RahulChaube_) · [EverestQ](https://www.everestqai.com/) · [Contact](https://www.rahulchaube1.com/contact)

[Blyx website](https://www.blyx-lang.space/) · [BlyxTorch](https://www.blyx-lang.space/packages/blyxtorch) · [Handbook](https://doc.blyx-lang.space/) · [Community](https://www.blyx-lang.space/community)

Support Rahul’s open-source work through [GitHub Sponsors](https://github.com/sponsors/Rahulchaube1) or [Buy Me a Coffee](https://buymeacoffee.com/rahulchaube).
