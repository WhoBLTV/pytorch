- This is the only AGENTS.md, there are no recursive AGENTS.md
- When you are working on a bug, first create a standalone file that
  reproduces the bug and verify it fails in the expected way.  Use this to
  test if your changes work.  Once the change is passing, find an appropriate
  test file to add the test to and make sure to follow local conventions on
  the test file.
- If you are running the real test suite, DO NOT run the entire test suite.
  Instead run only a single test case, e.g., 'python test/test_torch.py TestTorch.test_dir'
- Do NOT run setup.py or compile PyTorch from source. CPU binaries from the torch 2.10.0 wheel are overlaid on this tree (gitignored `*.so` files and `torch/version.py`). `python` and `pip` on PATH are the `/opt/pytorch-dev` virtualenv, and `import torch` loads `/workspace/torch`.
- Dev dependencies from `requirements.txt` are already installed. If `import torch` fails because shared libraries are missing, run `/opt/pytorch-dev/bin/python /opt/pytorch-dev/overlay_torch.py`.
- Do NOT run pre-commit, it is not setup
- To run lint, run `lintrunner init` once if needed, then `lintrunner -a` (which will autoapply changes)
- Do NOT create summary files unless explicitly asked
- When you are ready to make a PR, do exactly these steps:
  - git stash -u
  - git reset --hard $(cat /tmp/orig_work.txt) # NB: reset to the LOCAL branch, do NOT fetch
  - git stash pop
  - Resolve conflicts if necessary
