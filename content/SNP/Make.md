## basic rule & tabs

A target needs dependencies and a command. The command line **must** start with exactly one ASCII tab character.

```makefile
main.o: main.c header.h
	gcc -c main.c
```

## variables (= vs :=)

The `=` operator represents lazy evaluation (variable is expanded every time it is referenced), while `:=` represents immediate evaluation (value is expanded and fixed once at declaration).

```makefile
LDFLAGS = -lm
CFLAGS := -Wall -Wextra
```

## automatic variables

Shortcut variables that simplify rule writing. `$@` is the target name, `$^` is the entire dependency list, and `$<` is the first dependency name.

```diff
program: main.o utils.o
-	gcc -o program main.o utils.o
program: main.o utils.o
+	gcc -o $@ $^
```

## phony targets vs physical files

If a file named `clean` exists on disk, `make` may skip the command assuming it is up-to-date. Declaring `.PHONY` tells `make` the target is an action, not a file, forcing execution.

```makefile
.PHONY: clean
clean:
	-rm -f *.o program
```

## pattern rules & substitution

`$(SOURCES:%.c=%.o)` translates a source list into an object list. A suffix rule like `%.o: %.c` defines how to compile any `.o` from a matching `.c`.

```makefile
SOURCES = main.c utils.c
OBJECTS = $(SOURCES:%.c=%.o)

%.o: %.c
	gcc -c $< -o $@
```

## command silencing & error ignoring

The `@` prefix hides the command from the console. The `-` prefix tells `make` to ignore exit errors and continue the build.

```makefile
clean:
	-rm -f non_existent_file.o
	@echo "clean command run completed"
```

## command line options

`make -n` performs a dry-run. `make -k` continues compiling even if one module fails. `make -p` prints the entire internal database.

```bash
make -n
make -k
make -n -p | grep CFLAGS
```
