.PHONY: all build deploy rm rm-orphaned

NAMESPACE=factorio
CHART_NAME=factorio

# make-log: github.com/Noah-Huppert/make-log
NO_COLOR=\033[0m

OK_TAG=OK   #
OK_COLOR=\033[32;01m

WARN_TAG=WARN #
WARN_COLOR=\033[33;01m

ERROR_TAG=ERROR
ERROR_COLOR=\033[31;01m

define log = # level, message
$(if $(findstring ok, $(1)), @printf "$(OK_COLOR)[$(OK_TAG)] $(2)$(NO_COLOR)\n")
$(if $(findstring warn, $(1)), @printf "$(WARN_COLOR)[$(WARN_TAG)] $(2)$(NO_COLOR)\n")
$(if $(findstring error, $(1)), @printf "$(ERROR_COLOR)[$(ERROR_TAG)] $(2)$(NO_COLOR)\n")
endef

# all builds and deploys the chart 
all: build deploy

# build packages the external dns chart
build:
	$(call log, ok, Building chart)
	helm package .

# deploy pushes the external dns chart to the kubernetes cluster
# Args:
#	- HELM_ARGS: Additional Helm upgrade arguments to pass to the command
deploy: 
	$(call log, ok, Deploying chart)
	helm upgrade \
		--debug \
		--install \
		--namespace "${NAMESPACE}" \
		${HELM_ARGS} "${CHART_NAME}" .

# rm deletes the app deployment from the cluster
rm: 
	$(call log, ok, Deleting release)
	helm delete --purge "${CHART_NAME}"

# rm-orphaned removes all deployment resources manually in the event that they 
# have been orphaned during a failed install
rm-orphaned:
	$(call log, ok, Deleting Stateful Set)
	kubectl -n "${NAMESPACE}" delete statefulset "${CHART_NAME}" || true

	$(call log, ok, Deleting Service)
	kubectl -n "${NAMESPACE}" delete service "${CHART_NAME}" || true

	$(call log, ok, Deleting Ingress)
	kubectl -n "${NAMESPACE}" delete ingress "${CHART_NAME}" || true

	$(call log, ok, Deleting Persistent Volume Claim)
	kubectl -n "${NAMESPACE}" delete pvc "${CHART_NAME}-saves" || true
