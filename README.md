# Contribution Graph 📊

A simple Svelte 3 project to display a contribution graph with customizable squares representing activity levels over time.

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)

## Overview 📝

This project creates a contribution graph that visually represents activity levels for each day of the year. It uses Svelte 3 and Vite for fast and efficient development. The graph is displayed with different colored squares, each representing the level of activity for a particular day. Upon reloading the page, random contributions will be loaded to demonstrate the dynamic nature of the graph.

## Installation 🚀

1. Clone this repository to your local machine.
2. Navigate to the project directory.
3. Install the dependencies using npm:
   ```bash
   npm install
   ```
4. Start the development server:
   ```bash
   npm run dev
   ```
5. Open your web browser and go to http://localhost:5000 to see the contribution graph.

## Usage 🎨

The contribution graph can be customized by passing the `contributions` prop to the `ContributionGraph` component. The `contributions` prop should be an array of objects, where each object represents a day's data with the following format:

```javascript
{
  date: 'YYYY-MM-DD', // The date of the activity (e.g., '2023-07-25')
  count: 2, // The activity level for the day (should be a non-negative integer)
}
```

## Technologies Used 🛠️

- Svelte 3 - A modern JavaScript framework for building user interfaces.
- Vite - A fast development build tool and server with hot module replacement (HMR) support.

## License 📜

This project is licensed under the MIT License. See the [LICENSE](./LICENSE) file for details.

## Acknowledgements 👏

Special thanks to the [Svelte](https://svelte.dev/) and [Vite](https://vitejs.dev/) teams for their amazing tools.

## Get Involved 💬

Feel free to contribute, open issues, or provide suggestions to enhance this project. Let's make it even better together! 🌟

---

🔥 Happy coding! 🔥
