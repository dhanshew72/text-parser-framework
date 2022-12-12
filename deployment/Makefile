BUCKET=dh-deploys
STACK_NAME=text-parser-framework
PREFIX=${STACK_NAME}/${COMMIT_SHA}
OUTPUT_TEMPLATE_FILE=packaged.yaml

COMMIT_SHA=$$(git rev-parse --short HEAD)

package:
	aws cloudformation package \
		--template main.yaml \
  		--s3-bucket ${BUCKET} \
  		--s3-prefix ${PREFIX} \
  		--output-template-file ${OUTPUT_TEMPLATE_FILE}
  	# AWS Cloudformation deploy command doesn't support --template-url, but I want to keep a copy of this file in S3
	aws s3 cp packaged.yaml s3://${BUCKET}/${PREFIX}/packaged.yaml

deploy: package
	aws cloudformation deploy \
		--stack-name ${STACK_NAME} \
		--template-file ${OUTPUT_TEMPLATE_FILE} \
		--capabilities CAPABILITY_IAM
