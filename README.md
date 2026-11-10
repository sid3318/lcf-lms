# lcf-lms

Builds `ghcr.io/sid3318/lcf-lms`, the Frappe LMS image for learn.lungcarefoundation.org.

The official `ghcr.io/frappe/lms` images after v2.52.0 ship Frappe **without the LMS app**
([frappe/lms#2350](https://github.com/frappe/lms/issues/2350)), so `bench migrate` fails with
`No module named 'lms'`. This repo builds the same image with the app included, and refuses to
push it unless a smoke test finds the app.

## Use it in Dokploy

In the LMS service's Environment tab:

```
IMAGE_NAME=ghcr.io/sid3318/lcf-lms
VERSION=v15.0.0
```

## Upgrade

Edit `LMS_REF` (and `FRAPPE_BRANCH` if the release line changes) in `.github/workflows/build.yml`
and push to `main`. The image appears under the new tag after about 20 minutes. Then change `VERSION`
in Dokploy, back up, deploy, and run `bench --site all migrate`.

The package must be public (GitHub > Packages > lcf-lms > Package settings > Change visibility)
or Dokploy cannot pull it without registry credentials.
