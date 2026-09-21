# Safe test fixtures

These are deliberately harmless fixtures for exercising the scanner:

- `eicar.com` is the standard EICAR anti-malware test string. It is not malware,
  but security products intentionally report it as a test detection.
- `hello-linux-x86_64` is a locally built, no-op Linux ELF executable.
- `powershell-heuristic.txt` contains inert text that exercises one heuristic.

Do not use real malware samples in the repository. For malware validation,
use an isolated disposable VM and a separately managed, legally obtained test
corpus.

