# Known-password MD5 verification

This verification was performed during report preparation on 27 October 2026,
using the dummy password and JWT already present in the saved normal-login
capture. No request was sent to the application and no unknown password was cracked.

The screenshot from hash-identifier lists multiple possible algorithms. The
comparison below gives stronger evidence for this specific test-account value.

```text
MD5(UTF-8 dummy password) = 5de52ea9d787966e8b598720255a37a7
Disclosed JWT password   = 5de52ea9d787966e8b598720255a37a7
Exact match             = True
```

Reproduce against the saved evidence with Python:

```python
import base64
import hashlib
import json
import re
from pathlib import Path

capture = next(Path("evidence").glob("02*/*request_response.md"))
text = capture.read_text(encoding="utf-8-sig")
request = json.loads(re.search(r'\{"email"[^\n]+', text).group())
response = json.loads(re.search(r'\{"authentication"[^\n]+', text).group())
part = response["authentication"]["token"].split(".")[1]
payload = json.loads(base64.urlsafe_b64decode(part + "=" * (-len(part) % 4)))
calculated = hashlib.md5(request["password"].encode("utf-8")).hexdigest()
print("Calculated:", calculated)
print("Disclosed: ", payload["data"]["password"])
print("Match:     ", calculated == payload["data"]["password"])
```

This confirms the unsalted MD5 representation for the tested account. Database
storage and password-verification source code were not inspected.
