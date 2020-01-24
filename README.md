# labels-backup
back up of github labels, probably the latest ones

<!-- docks-start -->

_Generated using [jest-runner-docs](https://ghub.now.sh/jest-runner-docs)._

### [.parseHeader](./src/header.js#L28)

Parses given `header` string into an header object.
Basically the same as [.parse](#parse), except that
it only can accept single string and returns a `Header` object.

#### Signature

```ts
function(header, options)
```

#### Params

- `header` **{string}** - a header stirng like `'fix(foo): bar baz'`
- `returns` **{Header}** - a `Header` object like `{ type, scope?, subject }`

_The `parse*` methods are not doing any checking and validation,
so you may want to pass the result to `validateHeader` or `checkHeader`,
or to `validateHeader` with `ret` option set to `true`._

#### Example

```js
import { parseHeader } from 'parse-commit-message';

const longCommitMsg = `fix: bar qux

Awesome body!`;

const headerObj = parseCommit(longCommitMsg);
console.log(headerObj);
// => { type: 'fix', scope: null, subject: 'bar qux' }
```

### [.stringifyHeader](./src/header.js#L53)

Receives a `header` object, validates it using `validateHeader`,
builds a "header" string and returns it. Method throws if problems found.
Basically the same as [.stringify](#stringify), except that
it only can accept single `Header` object.

#### Signature

```ts
function(header, options)
```

#### Params

- `header` **{Header}** - a `Header` object like `{ type, scope?, subject }`
- `returns` **{string}** - a header stirng like `'fix(foo): bar baz'`



#### Example

```js
import { stringifyHeader } from 'parse-commit-message';

const headerStr = stringifyCommit({ type: 'foo', subject: 'bar qux' });
console.log(headerStr); // => 'foo: bar qux'
```

### [.validateHeader](./src/header.js#L106)

Validates given `header` object and returns `boolean`.
You may want to pass `ret` to return an object instead of throwing.
Basically the same as [.validate](#validate), except that
it only can accept single `Header` object.

#### Signature

```ts
function(header, options)
```

#### Params

- `header` **{Header}** - a `Header` object like `{ type, scope?, subject }`
- `returns` **{CommitResult}** - an object like `{ value: Array<Commit>, error: Error }`



#### Example

```js
import { validateHeader } from 'parse-commit-message';

const header = { type: 'foo', subject: 'bar qux' };

const headerIsValid = validateHeader(header);
console.log(headerIsValid); // => true

const { value } = validateHeader(header, true);
console.log(value);
// => {
//   header: { type: 'foo', scope: null, subject: 'bar qux' },
//   body: 'okey dude',
//   footer: null,
// }

const { error } = validateHeader({
  type: 'bar'
}, true);

console.log(error);
// => TypeError: header.subject should be non empty string
```

### [.checkHeader](./src/header.js#L147)

Receives a `Header` and checks if it is valid.
Basically the same as [.check](#check), except that
it only can accept single `Header` object.

#### Signature

```ts
function(header, options)
```

#### Params

- `header` **{Header}** - a `Header` object like `{ type, scope?, subject }`
- `options` **{object}** - options to control the header regex and case sensitivity
- `options.headerRegex` **{RegExp|string}** - string regular expression or instance of RegExp
- `options.caseSensitive` **{boolean}** - whether or not to be case sensitive, defaults to `false`
- `returns` **{Header}** - returns the same as given if no problems, otherwise it will throw.



#### Example

```js
import { checkHeader } from 'parse-commit-message';

try {
  checkHeader({ type: 'fix' });
} catch(err) {
  console.log(err);
  // => TypeError: header.subject should be non empty string
}

// throws because can accept only Header objects
checkHeader('foo bar baz');
checkHeader(123);
checkHeader([]);
checkHeader([{ type: 'foo', subject: 'bar' }]);
```

### [.parseCommit](./src/commit.js#L30)

Receives a full commit message `string` and parses it into an `Commit` object
and returns it.
Basically the same as [.parse](#parse), except that
it only can accept single string.

#### Signature

```ts
function(commit, options)
```

#### Params

- `commit` **{string}** - a message like `'fix(foo): bar baz\n\nSome awesome body!'`
- `returns` **{Commit}** - a standard object like `{ header: Header, body?, footer? }`

_The `parse*` methods are not doing any checking and validation,
so you may want to pass the result to `validateCommit` or `checkCommit`,
or to `validateCommit` with `ret` option set to `true`._

#### Example

```js
import { parseCommit } from 'parse-commit-message';

const commitObj = parseCommit('foo: bar qux\n\nokey dude');
console.log(commitObj);
// => {
//   header: { type: 'foo', scope: null, subject: 'bar qux' },
//   body: 'okey dude',
//   footer: null,
// }
```

### [.stringifyCommit](./src/commit.js#L61)

Receives a `Commit` object, validates it using `validateCommit`,
builds a "commit" string and returns it. Method throws if problems found.
Basically the same as [.stringify](#stringify), except that
it only can accept single `Commit` object.

#### Signature

```ts
function(commit, options)
```

#### Params

- `commit` **{Commit}** - a `Commit` object like `{ header: Header, body?, footer? }`
- `returns` **{string}** - a commit nessage stirng like `'fix(foo): bar baz'`

#### Example

```js
import { stringifyCommit } from 'parse-commit-message';

const commitStr = stringifyCommit({
  header: { type: 'foo', subject: 'bar qux' },
  body: 'okey dude',
});
console.log(commitStr); // => 'foo: bar qux\n\nokey dude'
```

### [.validateCommit](./src/commit.js#L108)

Validates given `Commit` object and returns `CommitResult`.
Basically the same as [.validate](#validate), except that
it only can accept single `Commit` object.

#### Signature

```ts
function(commit, options)
```

#### Params

- `commit` **{Commit}** - a `Commit` like `{ header: Header, body?, footer? }`
- `returns` **{CommitResult}** - an object like `{ value: Array<Commit>, error: Error }`

#### Example

```js
import { validateCommit } from 'parse-commit-message';

const commit = {
  header: { type: 'foo', subject: 'bar qux' },
  body: 'okey dude',
};

const commitIsValid = validateCommit(commit);
console.log(commitIsValid); // => true

const { value } = validateCommit(commit, true);
console.log(value);
// => {
//   header: { type: 'foo', scope: null, subject: 'bar qux' },
//   body: 'okey dude',
//   footer: null,
// }
```

### [.checkCommit](./src/commit.js#L145)

Receives a `Commit` and checks if it is valid. Method throws if problems found.
Basically the same as [.check](#check), except that
it only can accept single `Commit` object.

#### Signature

```ts
function(commit, options)
```

#### Params

- `commit` **{Commit}** - a `Commit` like `{ header: Header, body?, footer? }`
- `returns` **{Commit}** - returns the same as given if no problems, otherwise it will throw.

#### Example

```js
import { checkCommit } from 'parse-commit-message';

try {
  checkCommit({ header: { type: 'fix' } });
} catch (err) {
  console.log(err);
  // => TypeError: header.subject should be non empty string
}

// throws because can accept only Commit objects
checkCommit('foo bar baz');
checkCommit(123);
checkCommit([{ header: { type: 'foo', subject: 'bar' } }]);
```

<!-- docks-end -->
