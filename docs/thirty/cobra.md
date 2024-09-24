1、Command结构体简介

```go
	"github.com/spf13/cobra"

type Command struct {
	//Use (string)：该字段存储单行的使用说明。推荐的语法如下：
    //[] 表示可选参数，未被括号括起来的参数为必需参数。
    //... 表示可以为前一个参数指定多个值。
    //| 表示互斥信息，即只能使用左边或右边的参数，不能同时使用。
    //{} 表示一组互斥参数，其中一个是必需的；如果是可选的，则使用 []。
	// Example: add [-F file | -D dir]... [-f format] profile
	Use string

	// 该字段存储别名列表，可以用这些别名代替 Use 字段中的第一个单词。
	Aliases []string

    //"SuggestFor" 是一个数组，其中包含该命令将被建议执行的命令名称。
	// 与 Aliases 类似，但仅用于提供建议，而不是替代命令。
	SuggestFor []string

	// 命令的简短描述，会在 help 输出中显示。
	Short string

	// 该字段指定子命令在其父命令的 help 输出中所归类的组 ID。
	GroupID string

	// 命令的详细描述，通常会在 help <command> 中显示。
	Long string

	// 该字段存储命令的使用示例。
	Example string

	// 有效的非标志参数列表，通常用于 shell 自动补全。
	ValidArgs []string
	// 这是一个可选函数，提供用于 shell 自动补全的动态非标志参数。ValidArgs 和 ValidArgsFunction 只能选择一个使用。
	ValidArgsFunction func(cmd *Command, args []string, toComplete string) ([]string, ShellCompDirective)

	// 定义命令所期望的位置参数。
	Args PositionalArgs

	// 有效参数的别名列表，在 shell 自动补全中不建议使用，但可以手动输入。
	ArgAliases []string

	// 为旧版 bash 自动补全生成器自定义 bash 函数。建议使用 ValidArgsFunction 以提高与其他 shell 的兼容性。
	BashCompletionFunction string

	// 如果命令被废弃，该字段将定义废弃时的提示信息。
	Deprecated string

	// 键/值对，用于标识或分组命令，或设置特殊选项。
	Annotations map[string]string

	// Version定义该命令的版本。如果该值不为空并且命令没有定义“version”标志，则将在命令中添加一个“version”布尔标志，并且如果指定，将打印“version”变量的内容。如果命令没有定义一个简短的“v”标志，也会添加一个。
	Version string

	// The *Run functions are executed in the following order:
	//   * PersistentPreRun()
	//   * PreRun()
	//   * Run()
	//   * PostRun()
	//   * PersistentPostRun()
	// All functions get the same args, the arguments after the command name.
	// The *PreRun and *PostRun functions will only be executed if the Run function of the current
	// command has been declared.
	//
	// PersistentPreRun: children of this command will inherit and execute.
	PersistentPreRun func(cmd *Command, args []string)
	// PersistentPreRunE: PersistentPreRun but returns an error.
	PersistentPreRunE func(cmd *Command, args []string) error
	// PreRun: children of this command will not inherit.
	PreRun func(cmd *Command, args []string)
	// PreRunE: PreRun but returns an error.
	PreRunE func(cmd *Command, args []string) error
	// Run: Typically the actual work function. Most commands will only implement this.
	Run func(cmd *Command, args []string)
	// RunE: Run but returns an error.
	RunE func(cmd *Command, args []string) error
	// PostRun: run after the Run command.
	PostRun func(cmd *Command, args []string)
	// PostRunE: PostRun but returns an error.
	PostRunE func(cmd *Command, args []string) error
	// PersistentPostRun: children of this command will inherit and execute after PostRun.
	PersistentPostRun func(cmd *Command, args []string)
	// PersistentPostRunE: PersistentPostRun but returns an error.
	PersistentPostRunE func(cmd *Command, args []string) error

	// 指定哪些标志解析错误应该被忽略。
	FParseErrWhitelist FParseErrWhitelist

	// 控制 shell 自动补全的相关选项。
	CompletionOptions CompletionOptions

	// 执行子命令之前是否解析父命令的标志。
	TraverseChildren bool

	// 如果为 true，该命令将不会显示在可用命令列表中。
	Hidden bool

	// 如果为 true，将不会显示错误信息。
	SilenceErrors bool

	// 如果为 true，在发生错误时将不会显示使用信息。
	SilenceUsage bool

	// 禁用标志解析。如果为 true，所有标志将作为参数传递给common。
	DisableFlagParsing bool

	// 如果为 true，生成文档时将不会显示 "Auto generated by spf13/cobra..." 的标签。
	DisableAutoGenTag bool

	// 如果为 true，生成文档或帮助信息时将不会在命令的使用行添加 [flags]。
	DisableFlagsInUseLine bool

	// 如果为 true，将禁用基于 Levenshtein 距离的命令建议。
	DisableSuggestions bool

	// 指定显示命令建议的最小 Levenshtein 距离。
	SuggestionsMinimumDistance int
}
```

```go
CommondFlags().StringP()
CommondFlags().GetString()
```
