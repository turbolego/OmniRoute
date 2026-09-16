Fix friendliai "exhausted all your credits" 403 misclassification to quota_exhausted instead of auth_error.

FriendliAI returns HTTP 403 with body `{"detail":"You've exhausted all your credits..."}`
when free tier credits are depleted via Adaptive Rate Limits. This was being
misclassified as `AUTH_ERROR` instead of `QUOTA_EXHAUSTED`, causing omniroute
to not properly handle the credit exhaustion (treating it as a credential issue
rather than a depleted free tier).