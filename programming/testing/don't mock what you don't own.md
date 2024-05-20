---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://hynek.me/articles/what-to-mock-in-5-mins/

This article helped me understand the anti-mock viewpoint a bit; in fact it's not actually an anti-mock viewpoint at all, but rather an argument that you should raise the abstraction level to avoid spaghetti mocks.

Basically, he argues that this test, which mocks directly at the HTTP level does not convey intent:

```python
from unittest.mock import Mock
import httpx

def test_empty():
    client = Mock(
        spec_set=httpx.Client,
        get=Mock(
            return_value=Mock(
                spec_set=httpx.Response,
                json=lambda: {
                    "repositories": []
                },
            )
        ),
    )

    assert {} == get_repos_w_tags(client)
```

While this one, which tests the same thing but adds an abstraction layer above the HTTP request (and therefore _mocks what you own_ rather than the external interface), does:

```python
def test_empty_drc():
    drc = Mock(
        spec_set=DockerRegistryClient,
        get_repos=lambda: []
    )

    assert {} == get_repos_w_tags_drc(drc)
```