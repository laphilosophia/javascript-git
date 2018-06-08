Build git with javascript
----

This is a very basic implementation of Git version control system

This part implements basics of the following concepts:

1. Repository.
2. Commit.
3. Commit chaining.
4. Branch.

#

Here are some example codes.

```
console.log('Branch')

const repo = new Git('test')
repo.commit('Initial Commit')

// Maps the array of commits into a string of commit ids.
// For [C2, C1,C3], it returns "2-1-0"
function historyToIdMapper (history) {
	let ids = history.map(commit => {
		return commit.id
	})

	return ids.join('-')
}

// Should show 2 commits.
console.assert(historyToIdMapper(repo.log()) === '1-0')

repo.checkout('testing');
repo.commit('Change 3');

// Should show 3 commits.
console.assert(historyToIdMapper(repo.log()) === '2-1-0')

// Should show 2 commits. Master unpolluted.
repo.checkout('master');
console.assert(historyToIdMapper(repo.log()) === '1-0')

// Continue on master with 4th commit.
repo.commit('Change 3');
console.assert(historyToIdMapper(repo.log()) === '3-1-0')

```