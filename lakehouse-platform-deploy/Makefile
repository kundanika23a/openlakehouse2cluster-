.PHONY: lint syntax vault bootstrap preflight deploy test report

PLAYBOOKS := $(wildcard playbooks/*.yml)

lint:
	yamllint .
	ansible-lint

syntax:
	@set -e; for playbook in $(PLAYBOOKS); do ansible-playbook --syntax-check "$$playbook"; done

vault:
	ansible-vault create inventories/prod/group_vars/all/vault.yml

bootstrap:
	ansible-playbook playbooks/bootstrap.yml --ask-pass --ask-become-pass -e bootstrap_confirm=true

preflight:
	ansible-playbook playbooks/preflight.yml

deploy:
	ansible-playbook playbooks/site.yml

test:
	ansible-playbook playbooks/validate.yml

report:
	@echo "Gates have not passed. See reports/PROGRESS.md and reports/ENDPOINTS.md."
