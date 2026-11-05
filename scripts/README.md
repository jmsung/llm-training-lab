<!-- skeleton: optional/scripts/README.md — definition owned by harness; edit there, then run scripts/skeleton-sync.sh --fix -->
# scripts/ — entry points & orchestration

Runnable entry points and one-off orchestration: data prep, pipeline drivers,
experiment runners. Committed.

Test: *"Would I import this in a notebook or another script?"* **No** → it's a
script (hardcoded paths, `if __name__ == "__main__"`, side effects). **Yes** →
it belongs in the package (`src/<pkg>/`), imported by the script. Never duplicate
logic across scripts — factor shared code into the package.
