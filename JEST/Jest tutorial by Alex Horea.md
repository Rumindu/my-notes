* Jest is most popular testing frame work for js/ts
## Initialize TS project with Jest

1. Initialize empty node project `npm init
2. Then install those dependencies `npm i -D typescript jest ts-jest @types/jest ts-node`
	* `-D` for represent those are development dependencies.
3.  To initialize a configuration for ts-jest `npx ts-jest config:init`
	* It will create js file to confige the Jest. We will delete this file and create a file in Ts. `jest.config.ts`
	```js
		import type {Config} from '@jest/types'

		const config: Config.InitialOptions={ 
			preset: 'ts-jest',
			testEnvironment: 'node',
			verbose: true,//for show more info in console
		}

		export default config;
	```
4.  