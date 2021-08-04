# go-cheatsheet

useful go patterns when writing temporal.io stuff

## Control flow basics

### inline `err` assignment in `if`

```go
	if err := validateRolloverClusterCertInputs(input); err != nil {
		return output, err
	}
```


### for loop using `range`

```go
	for _, future := range futures {
		if err := future.Get(ctx, nil); err != nil {
			return output, err
		}
	}
```

## dynamic type stuff

### Defining struct methods

```go
type (
	rebootTemporal struct {
		logger log.Logger
    // no run method here
	}
)

func (c *rebootTemporal) run(ctx workflow.Context, input Foo) (Bar, error) {
  // ...
}

func SomeFn(ctx workflow.Context, input Foo) (Bar, error) {
  // ...
	c := &rebootTemporal{
		logger: workflow.GetLogger(ctx),
	}
	return c.run(ctx, input) // you can .run it!!
}

```
