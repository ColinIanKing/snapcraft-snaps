all: get_version set_version
	snapcraft

get_repo:
	@(if [ -d cppcheck ]; then \
		cd cppcheck; git pull; cd .. ; \
	else \
		git clone https://github.com/danmar/cppcheck.git;  \
	fi; > /dev/null) 2>&1 > /dev/null

get_version: get_repo
	@echo $(shell cd cppcheck; git tag | tail -1)-$(shell date +'%Y%m%d')-$(shell cd cppcheck; git log --oneline | wc -l)-$(shell cd cppcheck; git log -1 --oneline | cut -d' ' -f1) 

set_version:
	cat snapcraft.yaml | sed 's/version: .*/version: $(shell make get_version)/' > snapcraft-tmp.yaml
	mv snapcraft-tmp.yaml snapcraft.yaml

clean:
	rm -rf setup *.snap
	snapcraft clean
	cat snapcraft.yaml | sed 's/version: .*/version: 0/' > snapcraft-tmp.yaml
	mv snapcraft-tmp.yaml snapcraft.yaml
