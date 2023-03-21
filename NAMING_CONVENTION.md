# Naming Convention
## Contents
- [Code](#code)
    - [Files and Folders](#files-and-folders)
    - [Objects, Variables and Functions](#objects-variables-and-functions)
    - [Components Naming](#components-naming)
    - [Enums](#enums)
    - [Classes, Types and Interfaces](#classes-types-and-interfaces)
    - [Keys](#keys)
    - [Constants](#constants)

  CSS-in-JS Styles
    - [Methodology](#methodology)
- [GIT](#git)
    - [Main Rules](#main-rules)

## Code
#### Files and Folders

Use `camelCase` for names of **files** and **folders**. However, for **React components** it is ought to use `PascalCase`.
``` css
- components
    - IconButton.tsx
- styles
    - colors.ts
    - sizes.ts
```
#### Objects, Variables and Functions
Use `camelCase` when naming **objects**, **variables** and **functions** <ins>except functional components</ins>.
``` tsx
let thisIsMyCounter = 0;
const thisIsMyObject = {};
const thisIsMyFunction = () => {};

const SomeComponent: React.FC = () => {
    return <></>;
}
```
#### Components Naming
Use the **filename** as the **component name**. For example, `BookIcon.tsx` should
have a reference name of  `BookIcon`:
``` ts
import BookIcon from '@atoms/bookIcon/BookIcon';
import BookIcon from '@atoms/BookIcon';
```
#### Enums
Use `PascalCase` when naming **enums** and it’s **keys**.
``` ts
enum Mode {
    Contained = 'contained',
    Blank = 'blank',
}
```
#### Classes, Types and Interfaces
Use `PascalCase` when naming **types**, **interfaces** and **classes**.
``` ts
class User {
    constructor(options) {
        this.name = options.name;
    }
}
```
Also, use trailing letters `T` and `I` for **types** and **interfaces**.
``` ts
interface IButton {
    mode: Mode;
}
export type TMode = typeof Mode;
```
#### Keys
Use `camelCase` when naming objects', classes', types' and interfaces’ **keys** <ins>except ones for constants</ins>.
``` ts
interface IButton {
    mode: Mode;
    title: string;
    iconSize?: number;
}
```
#### Constants
Use `PascalCase` when naming **objects of constants** and `UPPER_CASE` for **constants**.
``` ts
const Stacks = {
    AUTH: '@STACKS_AUTH',
    MAIN: '@STACKS_MAIN',
};
const Screens = {
    Auth: {
        SIGN_IN: '@SCREENS_AUTH_SIGN_IN',
    },
}
```
### CSS-in-JS Styles
#### Methodology
We use BEM naming methodology as our base. Use `camelCase` for names consisting of several words.
``` css
blockName__elemName_modName_modValue
```
`blockName` is the name of the parent element, so "parentName" is used in below examples instead.
If there is no parent element for some element (this element is the parent for everything) its style would be named as:
``` css
elemName_modName_modValue
```
Thus, some imaginary nested structure could look like:
```
elemName
    elemName__elemName1
        elemName1__elemName2
            ...
```
Examples:
``` tsx
<View style={styles.wrapper}>
    <Image style={styles.wrapper__image}/>
</View>
```
``` tsx
<View style={styles.wrapper}>
    <View style={styles.wrapper__cover}>
        <Text style={styles.cover__title}/>
        <Image style={styles.cover__image}/>
    </View>
    <View style={styles.wrapper__content}>
        <Text style={styles.content__text} >...</Text>
        <Button style={
            styles.content__next, // for example if it is "go to the next page" button
        }/>
    </View>
</View>
```

We usually name Views that contain other views as "wrappers". Some nested wrappers examples:
```css
parentName__tagsWrapper
parentName__iconsWrapper
```
Try to make `elemName` understandable, it should describe the component where it is used fully, clearly.
If any similar component is added to the parent component there **must be no need to change your element's name**,
except you are exactly sure there won't be any similar components.

In the example above, the structure of the online reader is considered. The page displays
the title, the cover of the book and the text of the work. We know for sure that there can be only one title, image and
content text, so we might use `title, image, text` as elements names. However, this is a rare case, and there must be
an understandable parent name, therefore, it is preferable to name elements more complex.

#### Modifiers
`_modName_modValue`
Use modifier to describe style properties, that should be applied <ins>**only**</ins> when some condition applies.

For example:
- Style for case when component is **disabled**  `parentName__elemName_state_disabled`
- Style for cases when component has **contained mode**  `parentName__elemName_mode_contained`
``` tsx
<View
    style={[
        styles.wrapper,
        mode === 'contained' && styles.wrapper_mode_contained,
    ]}>
    <View style={styles.wrapper__cover}>
        <Text style={styles.cover__title}/>
        <Image style={styles.cover__image}/>
    </View>
    <View style={styles.wrapper__content}>
        <Text style={styles.content__text} >...</Text>
        <Button style={[
            styles.content__next, // for example if it is "go to the next page" button
            disabled && styles.content__next_state_disabled
        ]}/>
    </View>
</View>
```
## GIT
### Main Rules
1. Separate subject from body with a blank line
2. Limit the subject line to 50 characters
3. Capitalize the subject line
4. Do not end the subject line with a period
5. Use the imperative mood in the subject line
6. Wrap the body at 72 characters
7. Use the body to explain what and why vs. how
