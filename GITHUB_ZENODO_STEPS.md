# Publish to GitHub and mint a Zenodo DOI

## GitHub
1. Sign in to GitHub.
2. Click **New repository**.
3. Repository name: `Biomedical-LLM-GPU-Dangling-Centrality`.
4. Choose **Public**.
5. Do not initialize with a README if you will upload this prepared package.
6. Create the repository.
7. Upload the contents of this folder (not the outer ZIP itself if you want the files browsable).
8. Commit the upload.
9. On the repository page, choose **Releases -> Draft a new release**.
10. Create tag `v1.0.0`, title it `GTC 2027 reproducibility release`, and publish the release.

## Zenodo DOI
1. Sign in to Zenodo using your GitHub account.
2. In Zenodo GitHub settings, enable the new repository.
3. Because the GitHub release `v1.0.0` already exists, create a new GitHub release if Zenodo requires a post-enablement release (for example `v1.0.1`) or follow Zenodo's prompt to archive the existing release if offered.
4. Zenodo will create an archived record and DOI.
5. Copy the DOI into your README, CITATION.cff, and the poster's Code & Reproducibility box.
6. Generate a QR code from the final GitHub or Zenodo landing-page URL and place it on the poster.
