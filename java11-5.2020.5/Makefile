PAYARA_VERSION=5
PAYARA_RELEASE=2020.5
PAYARA_TAG=${PAYARA_VERSION}.${PAYARA_RELEASE}

image:
	docker build -t distroless-java-payara-micro:java11-${PAYARA_TAG} .
	@echo ""
	@echo "To test the image run:"
	@echo "docker run -it --rm --cpus 2 --memory 640m distroless-java-payara-micro:java11-${PAYARA_TAG}"

tag-and-push: image
	docker tag distroless-java-payara-micro:java11-${PAYARA_TAG} qaware/distroless-java-payara-micro:java11-${PAYARA_TAG}
	docker push qaware/distroless-java-payara-micro:java11-${PAYARA_TAG}
