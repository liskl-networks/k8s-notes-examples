# argocd-image-updater/

The examples of Field Guide 03, *Argo CD Image Updater on kind*, from the Kubernetes Notes zine series. The book runs
Argo CD Image Updater v1.4.0 on Field Guide 02's Argo CD v3.5.6 (this repo's folder `argocd/`, tag `argocd-1.0`) on
No. 00's kind lab. The pages pin the tag `argocd-image-updater-1.0`.

- `demo-image/`: the book's demo image, a static page that says which tag it is. The workflow
  `.github/workflows/argocd-image-updater-demo-image.yaml` builds and publishes one tag a run, to
  `ghcr.io/<owner>/k8s-notes-examples/image-updater-demo`.
- `deploy/kustomize/install/`: Image Updater's `install.yaml` for v1.4.0 as released (`bases/v1.4.0`, with its
  sha256), the lab's settings (`overlays/kind`), and the same with a `registries.conf` (`overlays/kind-registries`).
- `deploy/kustomize/roots/` and `cluster-manifests/overlays/`: the book's own root Application, `iu-root`, one hub
  per chapter that changes it (kind-ch02 to kind-ch11). It sits beside Field Guide 02's root.
- `deploy/kustomize/workloads/`: the apps Image Updater moves: `demo` (Kustomize, the book's image), `demo-set`
  (the same app for an ApplicationSet and the Source Hydrator) and `chart` (values for podinfo's own Helm chart).
- `deploy/kustomize/updaters/chNN/`: the ImageUpdater resources each chapter applies; `ch14/` is the failure gallery.
- `deploy/kustomize/appsets/`, `apps/`, `registries/`, `webhook/`: the ApplicationSet with and without its fix, the
  hydrated app, a `registries.conf` with a typo, and a GitHub `package` event for the webhook.

From chapter 8 the chapters write to Git: Image Updater's git write-back commits to the branch
`argocd-image-updater-lab`, and its pull request mode opens pull requests. Run those chapters in your own fork, on
that branch made from the tag, as the book says, and change `liskl` to your GitHub user where the files name it.
