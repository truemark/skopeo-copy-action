# Skopeo Copy Action

[![LICENSE](https://img.shields.io/badge/license-BSD3-green)](LICENSE)
[![Latest Release](https://img.shields.io/github/v/release/truemark/skopeo-copy-action)](https://github.com/truemark/skopeo-copy-action/releases)
![GitHub closed issues](https://img.shields.io/github/issues-closed/truemark/skopeo-copy-action)
![GitHub closed pull requests](https://img.shields.io/github/issues-pr-closed/truemark/skopeo-copy-action)
![build-test](https://github.com/truemark/skopeo-copy-action/workflows/build-test/badge.svg)

GitHub action used to start an SSH agent and add a private key to it.

## Examples

```yml
      - name: Login to ECR
        id: ecr-login
        uses: aws-actions/amazon-ecr-login@v1
        with:
          registry-type: public
      - name: Copy beta to ECR
        uses: truemark/skopeo-copy-action@616e8dff7e3d6792ea4ba033d49ab8fb1066c79a
        with:
          src-image: "docker://truemark/aws-cdk:beta"
          dest-image: "docker://public.ecr.aws/truemark/aws-cdk:beta"
          src-username: "${{ secrets.DOCKER_HUB_USERNAME }}"
          src-password: "${{ secrets.DOCKER_HUB_ACCESS_TOKEN }}"
          dest-username: "${{ steps.ecr-login.outputs.dockerUsername }}"
          dest-password: "${{ steps.ecr-login.outputs.dockerPassword }}"
          multi-arch: "all"
```

## Inputs

| Name           | Type       | Required | Description                                                              |
|----------------|------------|----------|--------------------------------------------------------------------------|
| src-image      | string     | Yes      | Source image                                                             |
| dest-image     | string     | Yes      | Destination image                                                        |
| src-username   | string     | Yes      | Source username                                                          |
| src-password   | string     | Yes      | Source password                                                          |
| dest-username  | string     | Yes      | Destination username                                                     |
| dest-password  | string     | Yes      | Destination password                                                     |
| multi-arch     | boolean    | No       | How to handle multi-arch images. System, all or index-only. Default: all |
| insecre-policy | boolean    | No       | Allow insecure TLS connections. Default: false                           |
