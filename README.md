# Cookbook serverspec

This cookbook is responsible for installing necessary gems, files, and tests in order to
use Serverspec. It only supports (as of 0.1.0) running Serverspec locally.

## Supported Platforms

Version 0.2.0 of this cookbook has been tested on Ubuntu 12.04 and Ubuntu 14.04.

## Attributes

<table>
<tr>
<th>Key</th>
<th>Type</th>
<th>Description</th>
<th>Default</th>
</tr>
<tr>
<td><tt>['serverspec']['directory']</tt></td>
<td>String</td>
<td>The root directory in which to place all Serverspec-related files</td>
<td><tt>/tmp/serverspec OR C:\serverspec</tt></td>
</tr>
<tr>
<td><tt>['serverspec']['logfile']</tt></td>
<td>String</td>
<td>The path and file name to write Serverspec results to</td>
<td><tt>/tmp/serverspec/serverspec.log</tt></td>
</tr>
<tr>
<td><tt>['serverspec']['gem_source']</tt></td>
<td>String</td>
<td>Configurable source location from which to download the serverspec gem</td>
<td><tt>https://rubygems.org</tt></td>
</tr>
<tr>
<td><tt>['serverspec']['gem_version']</tt></td>
<td>String</td>
<td>Version of the serverspec gem to install</td>
<td><tt>2.7.1</tt></td>
</tr>
</table>

## Usage

### serverspec::default

Include `serverspec` in your node's `run_list`:

```json
{
  "run_list": [
    "recipe[serverspec]"
    ]
}
```

This will add all necessary files, including the serverspec gem, to your machine to allow Serverspec to run.

To add your own tests, you can add each one using the `serverspec_test` LWRP:

```
serverspec_test 'example_spec.rb' do
source 'my_example_spec.rb'
end
```
NOTE: `example_spec.rb` is the name of the file on the machine, whereas `my_example_spec.rb` is the file in the `serverspec/files/default/...` directory.

### serverspec::run_tests

In order to run Serverspec tests, include the `run_tests` recipe:

```
{
  "run_list": [
    "recipe[serverspec::run_tests]"
    ]
}
```

### serverspec::cleanup

If you want to remove all traces of serverspec from the machine, include the `cleanup` recipe:

```
{
  "run_list": [
    "recipe[serverspec::cleanup]"
    ]
}
```

## Testing with Test Kitchen

A basic .kitchen.yml file was added for running the serverspec cookbook in Vagrant to test.
No kitchen tests were added, because tests are already handled by the default suite.

To run Test Kitchen:
```
kitchen test
```

## Author(s)

Author:: Jason Simmons (jasimmons90@gmail.com)
