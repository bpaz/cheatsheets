---
title: Cobra
layout: 2017/sheet
updated: 2017-11-27
category: golang
prism_languages: [go]
intro: > 
  [Cobra](https://github.com/spf13/cobra) is both a library for creating powerful modern CLI applications as well as a program to generate applications and command files.
---

{: .-no-hide}

## Installing

```shell
go get github.com/spf13/cobra/cobra
```

## Getting started

```go
cobra init <my_namespace>
```

## Commands

### Root command

```go
var rootCmd = &cobra.Command{
  Use:   "hugo",
  Short: "Hugo is a very fast static site generator",
  Long: `A Fast and Flexible Static Site Generator built with
                love by spf13 and friends in Go.`,
  Run: func(cmd *cobra.Command, args []string) {
    // Do Stuff Here
  },
}

func Execute() {
  if err := rootCmd.Execute(); err != nil {
    fmt.Println(err)
    os.Exit(1)
  }
}
```

### Sub commands

```go
package cmd

import (
  "fmt"

  "github.com/spf13/cobra"
)

func init() {
  rootCmd.AddCommand(versionCmd)
}

var versionCmd = &cobra.Command{
  Use:   "version",
  Short: "Print the version number of Hugo",
  Long:  `All software has versions. This is Hugo's`,
  Run: func(cmd *cobra.Command, args []string) {
    fmt.Println("Hugo Static Site Generator v0.9 -- HEAD")
  },
}
```

## Working with flags

### Persistent Flags

```go
rootCmd.PersistentFlags().BoolVarP(&Verbose, "verbose", "v", false, "verbose output")
```

### Local flags

```go
rootCmd.Flags().StringVarP(&Source, "source", "s", "", "Source directory to read from")
```

### Reqiored flags

```go
rootCmd.Flags().StringVarP(&Region, "region", "r", "", "AWS region (required)")
rootCmd.MarkFlagRequired("region")
```

## Positional arguments

### NoArgs

The command will report an error if there are any positional args.

### ArbitraryArgs 

The command will accept any args.

### MinimumNArgs(int) / MaximumNArgs (int)

The command will report an error if there are not at least N positional args.



References
----------

- <https://github.com/spf13/cobra>
