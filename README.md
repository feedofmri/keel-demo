# keel-demo

A small shop library with a test suite, used to demonstrate [Keel](https://keel.boraqs.com): when a change
breaks a test, Keel proposes a fix and opens a pull request labelled **AUTO-MERGE** or **NEEDS REVIEW**,
with the evidence for that decision.

## Set up with Keel

1. Sign in at [keel.boraqs.com](https://keel.boraqs.com) and install the Keel GitHub App on this repository.
2. Repositories → `keel-demo` → **Set up**: choose the models and risk level, and enter the model API key.
   Keel stores the key as an encrypted repository secret.
3. Merge the setup pull request. It adds `.keel.toml`, the Keel workflow and the shared calibration.

## Run the demo

```bash
git apply bugs/01-discount-backwards.patch   # one clear bug
git commit -am "Refactor discount maths" && git push
```

CI fails, the Keel workflow starts, and a pull request appears with the decision and its explanation.

```bash
git apply bugs/02-shipping-rules.patch       # two bugs, only one covered by the tests
git commit -am "Tweak shipping rules" && git push
```

Here a patch can pass every visible test and still be wrong; this is where Keel should ask for review.
You can also comment `/keel fix` on a pull request, or use **Fix now** in the Keel app.
