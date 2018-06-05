.PHONY: all build deploy rm

NAMESPACE=factorio
CHART_NAME=factorio

# all builds and deploys the chart
all: build deploy

# build packages the external dns chart
build:
	helm package .

# deploy pushes the external dns chart to the kubernetes cluster
deploy: 
	helm upgrade \
		--debug \
		--install \
		--namespace "${NAMESPACE}" \
		"${CHART_NAME}" .

# rm deletes the app deployment from the cluster
rm: 
	helm delete --purge "${CHART_NAME}"
