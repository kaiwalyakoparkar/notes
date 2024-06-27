# API Version

- `/v1` (Stable)
- `v1alpha1` (Recently Merged)
- `v1beta1` (Almost stable)

- When you query in the cluster the results are shown according to preffered version i.e v1
- Storage version is a version in which the object is stored in etcd
- Before returning results to you it is converted to v1
- Preferred version can be checked at `/apis/batch` endpoint
- Enable api groups in api-server at `--runtime-config=batch.v2aplha1`

# API Deprication

- API elements may only be removed by incrementing the version of API group
- API objects must be able to round-trip between API versions in a given release without information loss, with the exception of whole REST resources that do not exists in some versions.
- Other than the most recent API versions in each track, older API version must be supported after their announced deprication for duration of no less than
  - GA (12 month or 3 releases)
  - Beta (9 months or 3 releases)
  - Alpha (0 releases)
- The **preferred** API version and the **storage version** for a given group may not advance until after a release has been made that supports both the new version & previous versions.
- An API version is a given track may not be deprecated until a new API version at least as stable is released.

## Update Manifest versions

```bash
kubectl convert -f <filename> --output-version <version>
```