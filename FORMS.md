<!-- markdownlint-disable no-inline-html first-line-h1 -->

<p align="center">
  <img src="images/forms.png" alt="sass Logo" width="350" height="auto" />
</p>

# :dart: FORMS [Go Back](README.md)

## Creating Form in Ionic with Reactive Forms

Next, we will use `FormControl`, `FormGroup`, `FormBuilder`, and `Validators` service to validate the form data.

## FormGroup

A FormGroup is a collection of single or multiple FormControls and declared on the HTML’s form tag. Basically, its a collection of various form controls.

```html
<form [formGroup]="ionicForm" (ngSubmit)="submitForm()" novalidate>
</form>
```

## FormControl

A FormControl represents a value which is entered by the user, FormGroup is a collection of various FormControls

```html
<ion-content>
  <form [formGroup]="ionicForm" (ngSubmit)="submitForm()" novalidate>
    <ion-item lines="full">
      <ion-label position="floating">Name</ion-label>
      <ion-input formControlName="name" type="text"></ion-input>
    </ion-item>
    <span class="error ion-padding" *ngIf="isSubmitted && errorControl.name.errors?.required">
      Name is required.
    </span>
    <span class="error ion-padding" *ngIf="isSubmitted && errorControl.name.errors?.minlength">
      Name should be min 2 chars long.
    </span>
    <ion-row>
      <ion-col>
        <ion-button type="submit" color="danger" expand="block">Submit</ion-button>
      </ion-col>
    </ion-row>
  </form>
</ion-content>
```

## FormBuilder

 The FormBuilder service refers to a form object and sets up a FormGroup. It holds the user entered values and validation state of a form input field.

```typescript
import { Component, OnInit } from '@angular/core';
import { FormGroup, FormBuilder, Validators } from "@angular/forms";
@Component({
  selector: 'app-home',
  templateUrl: 'home.page.html',
  styleUrls: ['home.page.scss'],
})
export class HomePage implements OnInit {
  ionicForm: FormGroup;
  constructor(public formBuilder: FormBuilder) { }
}
```

## Validators

The Validators class offers following methods to deal with form validation in Ionic / Angular.

```typescript
class Validators {
  static min(min: number): ValidatorFn
  static max(max: number): ValidatorFn
  static required(control: AbstractControl): ValidationErrors | null
  static requiredTrue(control: AbstractControl): ValidationErrors | null
  static email(control: AbstractControl): ValidationErrors | null
  static minLength(minLength: number): ValidatorFn
  static maxLength(maxLength: number): ValidatorFn
  static pattern(pattern: string | RegExp): ValidatorFn
  ...
}
```

```html
<ion-header>
  <ion-toolbar>
    <ion-title>Ionic Forms</ion-title>
  </ion-toolbar>
</ion-header>
<ion-content>
  <form [formGroup]="ionicForm" (ngSubmit)="submitForm()" novalidate>
    <ion-item lines="full">
      <ion-label position="floating">Name</ion-label>
      <ion-input formControlName="name" type="text"></ion-input>
    </ion-item>
    <span class="error ion-padding" *ngIf="isSubmitted && errorControl.name.errors?.required">
      Name is required.
    </span>
<span class="error ion-padding"*ngIf="isSubmitted && errorControl.name.errors?.minlength">
      Name should be min 2 chars long.
    </span>
    <ion-row>
      <ion-col>
        <ion-button type="submit" color="danger" expand="block">Submit</ion-button>
      </ion-col>
    </ion-row>
  </form>
</ion-content>
```

```typescript
import { Component, OnInit } from '@angular/core';
import { FormGroup, FormBuilder, Validators } from "@angular/forms";
@Component({
  selector: 'app-home',
  templateUrl: 'home.page.html',
  styleUrls: ['home.page.scss'],
})
export class HomePage implements OnInit {
  ionicForm: FormGroup;
  constructor(public formBuilder: FormBuilder) { }
  ngOnInit() {
    this.ionicForm = this.formBuilder.group({
      name: ['', [Validators.required, Validators.minLength(2)]],
    })
  }
  get errorControl() {
    return this.ionicForm.controls;
  }
  submitForm() {
    this.isSubmitted = true;
    if (!this.ionicForm.valid) {
     // console.log('Please provide all the required!')
      return false;
    } else {
      //console.log(this.ionicForm.value)
    }
  }
}
```
