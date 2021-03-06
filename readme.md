# ngx-ow [![Build Status](https://travis-ci.org/SamVerschueren/ngx-ow.svg)](https://travis-ci.org/SamVerschueren/ngx-ow)

> Angular form validation on steroids

Use [Ow](https://github.com/sindresorhus/ow) to easily validate your Angular forms.


## Install

```
$ npm install ow ngx-ow
```


## Usage

[Ow API documentation](https://github.com/sindresorhus/ow#api) - [Example](https://stackblitz.com/edit/ngx-ow)

```ts
import {Component, OnInit} from '@angular/core';
import {owValidator} from 'ngx-ow';
import ow from 'ow';

@Component({
	selector: 'sign-up',
	templateUrl: 'sign-up.component.html'
})
export class SignUpComponent implements OnInit {
	form: FormGroup;

	constructor(
		private formBuilder: FormBuilder
	) {}

	ngOnInit() {
		this.form = this.formBuilder.group({
			firstName: ['', owValidator('firstNameRequired', ow.string.nonEmpty)],
			name: ['', owValidator('nameRequired', ow.string.nonEmpty)],
			email: ['', owValidator('emailInvalid', ow.string.nonEmpty.includes('@'))],
			password: ['', owValidator('passwordInvalid', ow.string.minLength(6))]
		});
	}
}
```

If someone enters an invalid email address, the errors object for the `email` control will look like this.

```json
{
	"emailInvalid": "Expected string to include `@`, got `hello`"
}
```


## Related

- [ow](https://github.com/sindresorhus/ow) - Function argument validation for humans.


## License

MIT © [Sam Verschueren](https://github.com/SamVerschueren)
