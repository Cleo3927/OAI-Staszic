PREVIEW ?= 0
LECTURE_SOURCES := $(wildcard *.qmd */*.qmd)
LECTURES := $(sort $(basename $(notdir $(LECTURE_SOURCES))))

.PHONY: all preview $(LECTURES)

all: $(LECTURES)

define QMD_FOR
$(firstword $(foreach file,$(LECTURE_SOURCES),$(if $(filter $(1),$(basename $(notdir $(file)))), $(file))))
endef

$(LECTURES):
	@src="$(call QMD_FOR,$@)"; \
	if [ -z "$$src" ]; then \
		echo "No .qmd source found for target '$@'." >&2; \
		exit 1; \
	fi; \
	if [ "$(PREVIEW)" = "1" ]; then \
		echo "Previewing $$src (Ctrl+C to stop)"; \
		quarto preview "$$src"; \
	else \
		echo "Rendering $$src"; \
		quarto render "$$src"; \
	fi

preview:
	@if [ -z "$(TARGET)" ]; then \
		echo "Usage: make preview TARGET=lecture_name" >&2; \
		exit 1; \
	fi
	@$(MAKE) $(TARGET) PREVIEW=1
