<!-- markdownlint-disable no-inline-html first-line-h1 -->

<p align="center">
  <img src="images/components.png" alt="sass Logo" width="300" height="auto" />
</p>

# :dart: Unit and E2E Testing [Go Back](README.md)

Example of unit and e2e testing

``` typescript
import { ComponentFixture } from '@angular/core/testing';
import { IonicModule } from '@ionic/angular';
import { ITestingModuleConfig, TestingUtils } from './test';

import { DemoPage } from './account.page';

describe('DemoPage', () => {
  let component: DemoPage;
  let fixture: ComponentFixture<DemoPage>;
  const config: ITestingModuleConfig = {
    components: [DemoPage],
    providers: [],
    imports: [IonicModule]
  };

  beforeEach(async () => {
    const compiled = await TestingUtils.beforeEachCompiler(config);
    fixture = compiled.fixture;
    component = compiled.instance;
    fixture.detectChanges();
  });

  afterEach(() => {
    fixture.destroy();
  });

  it('should create', () => {
    expect(component).toBeTruthy();
  });
});

```

Resource

### Ionic Framework Unit and E2E Testing

1. [Ionic Angular Unit Testing](https://ionicframework.com/docs/angular/testing)

### Unit test Tools

1. Jasmine (<https://jasmine.github.io/>)
2. Karma (<https://karma-runner.github.io/>)
3. Protractor (<https://www.protractortest.org/>)
4. Mocha (<https://mochajs.org/>)
5. Chai (<https://chaijs.com/>)
6. Sinon (<https://sinonjs.org/>)
7. Chai-as-promised (<https://www.chaijs.com/plugins/chai-as-promised/>)
8. Chai-things (<https://www.chaijs.com/plugins/chai-things/>)

### E2E test Tools

1. Cypress (<https://www.cypress.io/>) <b>Recommended</b>
2. BrowserStack (<https://www.browserstack.com/>) <b>Recommended</b>
3. Nightwatch (<https://nightwatchjs.org/>)
4. Selenium (<https://www.seleniumhq.org/>)
5. SauceLabs (<https://www.saucelabs.com/>)
6. TestingBot (<https://www.testingbot.com/>)
7. Appium (<https://appium.io/>)
8. PhantomJS (<https://www.phantomjs.org/>)
