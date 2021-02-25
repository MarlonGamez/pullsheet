# pullsheet

pullsheet generates a CSV (comma separated values) file containing metadata containing links and statistics about 
GitHub artifacts by a user or group of users across a series of GitHub repositories. It currently supports statistics on:

* Merged Pull Requests: `--kind=prs` (default)
* Pull Request Reviews: `--kind=reviews`
* Opening/Closing Issues: `--kind=issues`
* Issue Comments: `--kind=issue-comments`

This tool was created as a brain-tickler for what PR's to discuss when asking for that big promotion.

## Usage

`go run pullsheet --repos <repository> --since 2006-01-02 --token <github token> [--users=<user>]`

You will need a GitHub authentication token from https://github.com/settings/tokens

## Example: Merged PRs for 1 person across repos

`go run pullsheet.go --repos kubernetes/minikube,GoogleContainerTools/skaffold --since 2019-10-01 --token XXX --user someone > someone.csv`

## Example: Merged PR Reviews for all users in a repo

`go run pullsheet.go --repos kubernetes/minikube --kind=reviews --since 2020-12-24 --token XXX > reviews.csv`

## CSV fields

### Merged Pull Requests

```
	URL         string
	Date        string
	User        string
	Project     string
	Type        string
	Title       string
	Delta       int
	Added       int
	Deleted     int
	FilesTotal  int
	Files       string // newline delimited
	Description string
```

### Merged Pull Request Reviews

```
	URL            string
	Date           string
	Reviewer       string
	PRAuthor       string
	Project        string
	Title          string
	PRComments     int
	ReviewComments int
	Words          int
```

### Closed/Opened Issues

```
	URL     string
	Date    string
	Author  string
	Closer  string
	Project string
	Type    string
	Title   string
```

### Issue Comments

```
	URL         string
	Date        string
	Project     string
	Commenter   string
	IssueAuthor string
	IssueState  string
	Comments    int
	Words       int
	Title       string
```
