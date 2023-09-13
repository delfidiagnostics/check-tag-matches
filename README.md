# check-tag-matches
A simple github action to check that for an give docker image with the specified commit-id as a tag, it has a tag for the corresponding release candidate. If the specified tag match doesn't exist, the workflow is failed.

# Usage
Include the action as a step in your workflow. The worklfow will proceed if the tag matches otherwise it will be failed

```yaml
  pre-deploy-prod:
    name: Prod - Deploy Checks
    if: (github.event_name=='workflow_dispatch')
    runs-on: [ self-hosted, linux, X64 ]
    steps:
      - name: check tag matches
        id: check-tag
        uses: delfidiagnostics/check-tag-matches@X.X
        with:
          ecr_role_arn: arn:aws:iam::016272216798:role/ecr-rw-lis-repos
          ecr_repo_name: lis/example-repo
          image_id: 640d4bfde8e84759a37050b172f061fd11c1d621 #git commit hash of the stage build .e.g. 
          image_tag: 1.0.0 #git tag for the release version to be deployed to prod
```