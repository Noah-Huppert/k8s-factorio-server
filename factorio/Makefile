.PHONY: ftp factorio build deploy rm

MAKE=make
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

# ftp builds and deploys the chart with operating mode set to "ftp"
ftp:
	$(call log, ok, Starting FTP server)
	"${MAKE}" build
	"${MAKE}" HELM_ARGS="--set operatingMode=ftp" deploy

# factorio builds and deploys the chart with operating mode set to "factorio"
factorio:
	$(call log, ok, Starting Factorio server)
	"${MAKE}" build
	"${MAKE}" HELM_ARGS="--set operatingMode=factorio" deploy

# build packages the external dns chart
build:
	helm package .

# deploy pushes the external dns chart to the kubernetes cluster
# Args:
#	- HELM_ARGS: Additional Helm upgrade arguments to pass to the command
deploy: 
	helm upgrade \
		--debug \
		--install \
		--namespace "${NAMESPACE}" \
		${HELM_ARGS} "${CHART_NAME}" .

# rm deletes the app deployment from the cluster
rm: 
	helm delete --purge "${CHART_NAME}"
