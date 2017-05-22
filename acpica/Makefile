all: get_version set_version
	snapcraft

get_repo:
	@(if [ -d acpica ]; then \
		cd acpica; git pull; cd .. ; \
	else \
		git clone https://github.com/acpica/acpica ; \
	fi; > /dev/null) 2>&1 > /dev/null

get_version: get_repo
	@echo $(shell date +'%Y%m%d')-$(shell cd acpica; git tag | sed s/R// | sed s/_//g | tail -1)-$(shell cd acpica; git log --oneline | wc -l)-$(shell cd acpica; git log -1 --oneline | cut -d ' ' -f1 | cut -c1-7)

set_version:
	cat snapcraft.yaml | sed 's/version: .*/version: $(shell make get_version)/' > snapcraft-tmp.yaml
	mv snapcraft-tmp.yaml snapcraft.yaml

clean:
	rm -rf setup *.snap
	snapcraft clean
	cat snapcraft.yaml | sed 's/version: .*/version: 0/' > snapcraft-tmp.yaml
	mv snapcraft-tmp.yaml snapcraft.yaml
