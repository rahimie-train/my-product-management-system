
# PRODUCT-MANAGEMENT-SYSTEM

## Objective:
By the end of this session, students will be able to create class and functional components, style components using CSS, and perform CRUD operations in React using MockAPI. The project will be named "my-product-management-system" and will include pages to register categories and products.

## Agenda:
### 1. Introduction (10 minutes)
- Overview of React components: class components vs functional components.
- Introduction to React's component lifecycle methods.
- Brief introduction to CSS in React.
- Introduction to MockAPI for CRUD operations.

### 2. Setting Up the Project (5 minutes)
- Create a new React project using Create React App.
- Start the React development server.
- Brief overview of the project's folder structure.

```bash
npx create-react-app my-product-management-system
cd my-product-management-system
npm start
```



### 3. Editing App.js (3 minutes)
- Modify \`App.js\` to include set title project / Hello World! to test this app.js page

```bash
import React from 'react';
import { BrowserRouter as Router, Route, Link } from 'react-router-dom';
import CategoryFormClass from './components/Category/CategoryFormClass';
import ProductFormClass from './components/Product/ProductFormClass';

function App() {
  return (
    <Router>
      <div className="App">
        <h1>Product Management System</h1>
      </div>
    </Router>
  );
}

export default App;
```
### 4. Setting Up the Project Folder Structure / File System (10 minutes) 
- Create folder and file according to below file structure page
- Brief overview of the project's folder structure.

```bash
my-product-management-system/
├── public/
│   ├── index.html
│   └── ...
├── src/
│   ├── components/
│   │   ├── Category/
│   │   │   ├── CategoryFormClass.js
│   │   │   ├── CategoryListClass.js
│   │   │   ├── CategoryFormFunction.js
│   │   │   ├── CategoryListFunction.js
│   │   │   ├── Category.css
│   │   ├── Product/
│   │   │   ├── ProductListClass.js
│   │   │   ├── ProductFormClass.js
│   │   │   ├── ProductListFunction.js
│   │   │   ├── ProductFormFunction.js
│   │   │   ├── Product.css
│   ├── services/
│   │   ├── ApiCategory.js
│   │   ├── ApiProduct.js
│   ├── App.js
│   ├── index.js
│   └── ...
├── package.json
└── ...
```

### 5. Creating Class Components (30 minutes)
- Deep dive into creating class components.
- Create `CategoryFormClass.js` and `CategoryListClass.js` as class components.
- Discuss state management, event handling, and lifecycle methods.
  
CategoryFormClass.js 



##### I: Importing Dependencies

Start by importing React and any necessary services:

```
import React, { Component } from 'react';
```

#### II: Defining the Class Component

```
class CategoryFormClass extends Component {
    state = {
        name: '',
        description: ''
    };
    render() {
        return (
            "test"
      );
    }
}     
```

#### III: Exporting the Component

```
export default CategoryFormClass;

```

#### IV: Handling Input Changes & Submit Function
```
handleChange = (event) => {
  this.setState({ [event.target.name]: event.target.value });
};

handleSubmit = (event) => {
    event.preventDefault();
    const { name, description } = this.state;
    console.log(this.state);
    alert(`Category Name: ${name}\nCategory Description: ${description}`);

    this.setState({ name: "", description: "" });

    // Call the addCategory method passed down from CategoryListClass
    // this.props.addCategory({ name, description }); 
    // API integration will be handled in the next chapter
    // await createCategory({ name, description });
    // this.props.fetchCategories();
};

```
```
//   handleSubmit = (event) => {
//     event.preventDefault();
//     const { name, description } = this.state;
//     console.log(this.state);
//     alert(`Category Name: ${name}\nCategory Description: ${description}`);

//     this.setState({ name: "", description: "" });

//     // Call the addCategory method passed down from CategoryListClass
//     this.props.addCategory({ name, description }); 

//     // Call the createCategory function, which uses axios to create a new category
//     createCategory({ name, description })
//         .then(response => {
//             console.log("Category created successfully:", response.data);
//             // Optionally, you could call fetchCategories here if you want to refresh the category list
//             // this.props.fetchCategories();
//         })
//         .catch(error => {
//             console.error("There was an error creating the category:", error);
//         });
//     };
```
#### V: Rendering the Form
```
render() {
  const { name, description } = this.state;

  return (
    <form onSubmit={this.handleSubmit}>
      <input
        type="text"
        name="name"
        value={name}
        onChange={this.handleChange}
        placeholder="Category Name"
      />
      <input
        type="text"
        name="description"
        value={description}
        onChange={this.handleChange}
        placeholder="Category Description"
      />
      <button type="submit">Add Category</button>
    </form>
  );
}

```


<details>
  <summary>full code</summary>

  ```jsx
  import React, { Component } from 'react';
  import { createCategory } from '../../services/ApiCategory';

  class CategoryFormClass extends Component {
    state = {
      name: '',
      description: ''
    };

    handleChange = (event) => {
      this.setState({ [event.target.name]: event.target.value });
    };

    handleSubmit = async (event) => {
      event.preventDefault();
      const { name, description } = this.state;
      await createCategory({ name, description });
      this.setState({ name: '', description: '' });
      this.props.fetchCategories();
    };

    render() {
      const { name, description } = this.state;

      return (
        <form onSubmit={this.handleSubmit}>
          <input
            type="text"
            name="name"
            value={name}
            onChange={this.handleChange}
            placeholder="Category Name"
          />
          <input
            type="text"
            name="description"
            value={description}
            onChange={this.handleChange}
            placeholder="Category Description"
          />
          <button type="submit">Add Category</button>
        </form>
      );
    }
  }

  export default CategoryFormClass;
```
</details>


CategoryListClass.js


#### I: Importing Dependencies

Start by importing React and any necessary services:

```
import React, { Component } from 'react';
import './Category.css';
import CategoryFormClass from './CategoryFormClass';
// import { getCategories, deleteCategory, updateCategory } from '../../services/ApiCategory';
```

#### II: Defining the Class Component and Initial State


```
class CategoryListClass extends Component {
  state = {
    categories: [
      // Hardcoded categories for initial testing
      { id: 1, name: "Electronics", description: "Devices and gadgets" },
      { id: 2, name: "Books", description: "Various books and literature" },
    ],
    isEditing: false,
    currentCategory: { id: "", name: "", description: "" },
  };

  render() {
    return "test";
  }
}
```

#### III: Lifecycle Method and Fetch Categories


```
componentDidMount() {
  // this.fetchCategories();
}

fetchCategories = async () => {
  // const categories = await getCategories();
  // this.setState({ categories });
};


```

#### IV: Handling Delete, Edit, and Cancel Edit
```
handleDelete = (id) => {
  const filteredCategories = this.state.categories.filter(category => category.id !== id);
  this.setState({ categories: filteredCategories });
  console.log(id);
  alert(`Deleted Id: ${id}`);
  // await deleteCategory(id);
  // this.fetchCategories();
};

handleEdit = (category) => {
  this.setState({ isEditing: true, currentCategory: category });
};

handleCancelEdit = () => {
  this.setState({ isEditing: false, currentCategory: { id: '', name: '', description: '' } });
};

```
#### V: Handling Input Changes and Update and Add using props
```
handleChange = (event) => {
  const { name, value } = event.target;
  this.setState((prevState) => ({
    currentCategory: { ...prevState.currentCategory, [name]: value }
  }));
};

handleUpdate = (event) => {
    event.preventDefault();

    const { categories, currentCategory } = this.state;

    const updatedCategories = categories.map((category) =>
      category.id === currentCategory.id ? { ...currentCategory } : category
    );

    this.setState({
      categories: updatedCategories,
      isEditing: false,
      currentCategory: { id: "", name: "", description: "" },
    });

    alert(`Category Name: ${currentCategory.name}\nCategory Description: ${currentCategory.description}`);
    console.log(this.state);
    
    // await updateCategory(currentCategory.id, { name: currentCategory.name, description: currentCategory.description });
    // this.fetchCategories();
};

addCategory = (newCategory) => {
    this.setState((prevState) => ({
      categories: [...prevState.categories, { id: prevState.categories.length + 1, ...newCategory }],
    }));
};
```

#### VI: Rendering the Component

```
render() {
  const { categories, isEditing, currentCategory } = this.state;
  return (
    <div>
      <h2>Categories</h2>
      {isEditing ? (
        <form onSubmit={this.handleUpdate}>
          <input
            type="text"
            name="name"
            value={currentCategory.name}
            onChange={this.handleChange}
            placeholder="Category Name"
          />
          <input
            type="text"
            name="description"
            value={currentCategory.description}
            onChange={this.handleChange}
            placeholder="Category Description"
          />
          <button type="submit" className="button button-update">Update</button>
          <button type="button" className="button button-delete" onClick={this.handleCancelEdit}>Cancel</button>
        </form>
      ) : (
         <CategoryFormClass addCategory={this.addCategory} />
        // <CategoryFormClass fetchCategories={this.fetchCategories} />
      )}
     <div style={{ display: "inline-block", textAlign: "left", marginTop: "20px"}}>
        <table>
          <thead>
            <tr>
              <th>ID</th>
              <th>Name</th>
              <th>Description</th>
              <th>Actions</th>
            </tr>
          </thead>
          <tbody>
            {categories.map(category => (
              <tr key={category.id}>
                <td>{category.id}</td>
                <td>{category.name}</td>
                <td>{category.description}</td>
                <td>
                  <button className="button button-update" onClick={() => this.handleEdit(category)}>Edit</button>
                  <button className="button button-delete" onClick={() => this.handleDelete(category.id)}>Delete</button>
                </td>
              </tr>
            ))}
          </tbody>
        </table>
      </div>
    </div>
  );
}
```


#### VI: Exporting the Component

```
export default CategoryListClass;

```


<details>
  <summary>full code</summary>

  ```jsx
  import React, { Component } from 'react';
// import { getCategories, deleteCategory, updateCategory } from '../../services/ApiCategory';
import './Category.css';
import CategoryFormClass from './CategoryFormClass';

class CategoryListClass extends Component {
  state = {
    categories: [
      { id: 1, name: 'Electronics', description: 'Devices and gadgets' },
      { id: 2, name: 'Books', description: 'Various books and literature' }
    ],
    isEditing: false,
    currentCategory: { id: '', name: '', description: '' },
  };

  // componentDidMount() {
  //   this.fetchCategories();
  // }

  // fetchCategories = async () => {
  //   const categories = await getCategories();
  //   this.setState({ categories });
  // };

  handleDelete = (id) => {
    const filteredCategories = this.state.categories.filter(category => category.id !== id);
    this.setState({ categories: filteredCategories });
  };

  handleEdit = (category) => {
    this.setState({ isEditing: true, currentCategory: category });
  };

  handleCancelEdit = () => {
    this.setState({ isEditing: false, currentCategory: { id: '', name: '', description: '' } });
  };

  handleChange = (event) => {
    const { name, value } = event.target;
    this.setState((prevState) => ({
      currentCategory: { ...prevState.currentCategory, [name]: value }
    }));
  };

  handleUpdate = (event) => {
    event.preventDefault();
    const { categories, currentCategory } = this.state;
    const updatedCategories = categories.map(category =>
      category.id === currentCategory.id
        ? { ...currentCategory }
        : category
    );
    this.setState({ categories: updatedCategories, isEditing: false, currentCategory: { id: '', name: '', description: '' } });
  };

  render() {
    const { categories, isEditing, currentCategory } = this.state;
    return (
      <div>
        <h2>Categories</h2>
        {isEditing ? (
          <form onSubmit={this.handleUpdate}>
            <input
              type="text"
              name="name"
              value={currentCategory.name}
              onChange={this.handleChange}
              placeholder="Category Name"
            />
            <input
              type="text"
              name="description"
              value={currentCategory.description}
              onChange={this.handleChange}
              placeholder="Category Description"
            />
            <button type="submit" className="button button-update">Update</button>
            <button type="button" className="button button-delete" onClick={this.handleCancelEdit}>Cancel</button>
          </form>
        ) : (
          <CategoryFormClass fetchCategories={this.fetchCategories} />
        )}
        <table>
          <thead>
            <tr>
              <th>ID</th>
              <th>Name</th>
              <th>Description</th>
              <th>Actions</th>
            </tr>
          </thead>
          <tbody>
            {categories.map(category => (
              <tr key={category.id}>
                <td>{category.id}</td>
                <td>{category.name}</td>
                <td>{category.description}</td>
                <td>
                  <button className="button button-update" onClick={() => this.handleEdit(category)}>Edit</button>
                  <button className="button button-delete" onClick={() => this.handleDelete(category.id)}>Delete</button>
                </td>
              </tr>
            ))}
          </tbody>
        </table>
      </div>
    );
  }
}

export default CategoryListClass;


  ```
</details>


### 6. Adding CSS (15 minutes)
- Demonstrate how to add and apply CSS in React.
- Style the category and product forms.
 Category.css *
```css
  form {
     margin: 20px;
  }

   input {
    margin-right: 10px;
  }

  table {
    width: 100%;
    border-collapse: collapse;
    margin: 20px 0;
    font-size: 18px;
    text-align: left;
  }
  
  th, td {
    padding: 12px 15px;
    border: 1px solid #ddd;
  }
  
  th {
    background-color: #f4f4f4;
  }
  
  tr:nth-child(even) {
    background-color: #f9f9f9;
  }
  
  tr:hover {
    background-color: #f1f1f1;
  }
  
  .button {
    color: white;
    border: none;
    padding: 5px 10px;
    cursor: pointer;
  }
  
  .button-delete {
    background-color: #ff4d4d;
  }
  
  .button-delete:hover {
    background-color: #ff1a1a;
  }
  
  .button-update {
    background-color:blue;
  }
  
  .button-update:hover {
    background-color: blue;
  }
  
```
### 7. Integrating MockAPI for CRUD Operations (20 minutes)
- Set up MockAPI for category and product management.
- Perform CRUD operations (Create, Read, Update, Delete) using MockAPI.
- Url Localhost / Mockapi: 'https://66b1b4381ca8ad33d4f4d9c0.mockapi.io/api/v1/category';
- Discuss Axios/ Await Fectch
- **Install React Router:**
```bash
   npm install axios --save
```
- ApiCategory.js
```jsx
import axios from 'axios';

const apiUrl = 'https://66b1b4381ca8ad33d4f4d9c0.mockapi.io/api/v1/category';

export const getCategories = () => {
  return axios.get(apiUrl)
    .then((response) => response.data);
};

export const createCategory = (category) => {
  return axios.post(apiUrl, category)
    .then((response) => response.data);
};

export const deleteCategory = (id) => {
  return axios.delete(`${apiUrl}/${id}`)
    .then((response) => response.data);
};

export const updateCategory = (id, category) => {
  return axios.put(`${apiUrl}/${id}`, category)
    .then((response) => response.data);
};


// Example with custom headers
// export const createCategory = (category, token) => {
//     return axios.post(apiUrl, category, {
//       headers: {
//         Authorization: `Bearer ${token}` // Example of an auth token
//       }
//     }).then((response) => response.data);
//   };

// export const createCategory = (category) =>
//     fetch(apiUrl, {
//       method: 'POST',
//       headers: {
//         'Content-Type': 'application/json',
//       },
//       body: JSON.stringify(category),
//     }).then((res) => res.json());
  
//   export const deleteCategory = (id) =>
//     fetch(\`\${apiUrl}/\${id}\`, {
//       method: 'DELETE',
//     }).then((res) => res.json());
  
//   export const updateCategory = (id, category) =>
//     fetch(\`\${apiUrl}/\${id}\`, {
//       method: 'PUT',
//       headers: {
//         'Content-Type': 'application/json',
//       },
//       body: JSON.stringify(category),
//     }).then((res) => res.json());
  
```




### 8. Routing Navigation (15 minutes)

- Discus how React Rauter works
- Modify \`App.js\` to include a welcome message and links to the category and product registration pages.
- Step-by-Step Instructions:
    -  **Install React Router:**
    -  Run the following command to install React Router:
   ```bash
   npm install react-router-dom
   ```

  - **Modify App.js:**
   - Replace the content of \`App.js\` with the following code:
   ```jsx
  import React from 'react';
  import { BrowserRouter as Router, Route, Routes, Link } from 'react-router-dom';
  import logo from './logo.svg';
  import './App.css';
  import CategoryListClass from './components/Category/CategoryListClass';
  
  function App() {
    return (
      <Router>
        <div className="App">
          <h1>Product Management System</h1>
          <nav>
            <ul>
              <li>
                <Link to="/category">Register Category</Link>
              </li>
              <li>
                <Link to="/product">Register Product</Link>
              </li>
            </ul>
          </nav>
          <Routes>
            <Route path="/category" element={<CategoryListClass />} />
            <Route path="/product" element={<CategoryListClass />} />
          </Routes>
        </div>
      </Router>
    );
  }
  
  export default App;

   ```

   
### 9. Design Content Navigation (15 minutes)
- Modify \`App.js\` to design topbar,sidebar and contentregistration pages.
- Step-by-Step Instructions:
    -  **Modify App.js:**
    -  Replace code to App.js:
  ```jsx 
    import logo from './logo.svg';
    import './App.css';
    import CategoryListClass from './components/Category/CategoryListClass';
    import { BrowserRouter as Router, Link, Route, Routes } from 'react-router-dom';
    
    function App() {
      return (
        <Router>
          <div className="App">
            <div className="topbar">
              <h1>Product Management System</h1>
            </div>
            <div className="container">
              <nav className="sidebar">
                <ul>
                  <li>
                    <Link to="/category1">Category</Link>
                  </li>
                  <li>
                    <Link to="/product">Product</Link>
                  </li>
                </ul>
              </nav>
              <div className="content">
                <Routes>
                  <Route path="/category1" element={<CategoryListClass />} />
                  {/*<Route path="/product" element={<ProductList />} /> */}
                </Routes>
              </div>
            </div>
          </div>
        </Router>
      );
    }
    
    export default App;


   ```


  - **Modify App.css:**
   - Add the content of \`App.css\` with the following code:
   ```css 
    .App {
        font-family: sans-serif;
        text-align: center;
        display: flex;
        flex-direction: column;
        height: 100vh;
    }

    .topbar {
        background-color: #f8f9fa;
        box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
        padding: 20px;
    }

    .container {
        display: flex;
        flex-grow: 1;
    }

    .sidebar {
        width: 200px;
        background-color: #f8f9fa;
        padding: 15px;
        box-shadow: 2px 0 5px rgba(0, 0, 0, 0.1);
        text-align: left;
    }

    .sidebar ul {
        list-style-type: none;
        padding: 0;
    }

    .sidebar ul li {
        margin: 10px 0;
    }

    .sidebar ul li a {
        text-decoration: none;
        color: #007bff;
        font-weight: bold;
    }

    .content {
        flex-grow: 1;
        padding: 40px;
    }

   ```
   
### 10. Break (5 minutes)
### 11. Creating Functional Components (30 minutes)
- Deep dive into creating functional components with hooks.
- Create `CategoryFormFunction.js` and `CategoryListFunction.js` as functional components.
- Discuss useState and useEffect hooks.
CategoryFormFunction.js
```jsx
import React, { useState } from 'react';
import { createCategory } from '../../services/ApiCategory';

const CategoryFormFunction = ({ fetchCategories }) => {
  const [categoryName, setCategoryName] = useState('');
  const [description, setDescription] = useState('');

  const handleChange = (event) => {
    const { name, value } = event.target;
    if (name === 'name') setCategoryName(value);
    if (name === 'description') setDescription(value);
  };

  const handleSubmit = async (event) => {
    event.preventDefault();
    await createCategory({ name: categoryName, description });
    setCategoryName('');
    setDescription('');
    fetchCategories();
  };

  return (
    <form onSubmit={handleSubmit}>
      <input
        type="text"
        name="name"
        value={categoryName}
        onChange={handleChange}
        placeholder="Category Name"
      />
      <input
        type="text"
        name="description"
        value={description}
        onChange={handleChange}
        placeholder="Category Description"
      />
      <button type="submit">Add Category</button>
    </form>
  );
};

export default CategoryFormFunction;
```
CategoryListFunction.js
```jsx
import React, { useEffect, useState } from 'react';
import { getCategories, deleteCategory, updateCategory } from '../../services/ApiCategory';
import './Category.css';
import CategoryFormFunction from './CategoryFormFunction';

const CategoryListFunction = () => {
  const [categories, setCategories] = useState([]);
  const [isEditing, setIsEditing] = useState(false);
  const [currentCategory, setCurrentCategory] = useState({ id: '', name: '', description: '' });

  useEffect(() => {
    fetchCategories();
  }, []);

  const fetchCategories = async () => {
    const categories = await getCategories();
    setCategories(categories);
  };

  const handleDelete = async (id) => {
    await deleteCategory(id);
    fetchCategories();
  };

  const handleEdit = (category) => {
    setIsEditing(true);
    setCurrentCategory(category);
  };

  const handleCancelEdit = () => {
    setIsEditing(false);
    setCurrentCategory({ id: '', name: '', description: '' });
  };

  const handleChange = (event) => {
    const { name, value } = event.target;
    setCurrentCategory((prevCategory) => ({
      ...prevCategory,
      [name]: value,
    }));
  };

  const handleUpdate = async (event) => {
    event.preventDefault();
    await updateCategory(currentCategory.id, {
      name: currentCategory.name,
      description: currentCategory.description,
    });
    setIsEditing(false);
    setCurrentCategory({ id: '', name: '', description: '' });
    fetchCategories();
  };

  return (
    <div>
      <h2>Categories</h2>
      {isEditing ? (
        <form onSubmit={handleUpdate}>
          <input
            type="text"
            name="name"
            value={currentCategory.name}
            onChange={handleChange}
            placeholder="Category Name"
          />
          <input
            type="text"
            name="description"
            value={currentCategory.description}
            onChange={handleChange}
            placeholder="Category Description"
          />
          <button type="submit" className="button button-update">
            Update
          </button>
          <button type="button" className="button button-delete" onClick={handleCancelEdit}>
            Cancel
          </button>
        </form>
      ) : (
        <CategoryFormFunction fetchCategories={fetchCategories} />
      )}
      <table>
        <thead>
          <tr>
            <th>ID</th>
            <th>Name</th>
            <th>Description</th>
            <th>Actions</th>
          </tr>
        </thead>
        <tbody>
          {categories.map((category) => (
            <tr key={category.id}>
              <td>{category.id}</td>
              <td>{category.name}</td>
              <td>{category.description}</td>
              <td>
                <button className="button button-update" onClick={() => handleEdit(category)}>
                  Edit
                </button>
                <button className="button button-delete" onClick={() => handleDelete(category.id)}>
                  Delete
                </button>
              </td>
            </tr>
          ))}
        </tbody>
      </table>
    </div>
  );
};

export default CategoryListFunction;
```



### 12. Task to Create Product Page (60 minutes)
- Follow category page, task to create product registration page. Can use class / functional component
- Link forms to MockAPI for data submission.
- Url localhost / Mockapi: 'https://66b1b4381ca8ad33d4f4d9c0.mockapi.io/api/v1/product';
- Implement similar logic for \`ProductForm.js\` &  \`ProductList.js\`
Example form and list structure with API integration
```jsx
import React, { Component } from 'react';
import ProductForm from './ProductForm';
import { deleteProduct, updateProduct, getProduct } from '../../services/ApiProduct';
import './Product.css';

class ProductList extends Component {
  state = {
    products: [],
    isEditing: false,
    currentProduct: { id: '', name: '', description: '', category: '' },
  };

  componentDidMount() {
  }

  render() {   
  }
}

export default ProductList;

```





## Conclusion (15 minutes)
- Recap the key concepts covered.
- Q&A session to address any doubts or questions.
- Provide resources for further learning.

## Resources:
- [React Documentation](https://reactjs.org/docs/getting-started.html)
- [MockAPI Documentation](https://mockapi.io/docs)
- [CSS Tricks](https://css-tricks.com/)
- [React Router Documentation](https://reactrouter.com/web/guides/quick-start)


## Prerequisite Topics
- [Explore project files and folders](https://reactjs.org/docs/getting-started.html)
- [Write basic JSX elements](https://reactjs.org/docs/introducing-jsx.html)
- [Practice embedding expressions and adding attributes](https://reactjs.org/docs/introducing-jsx.html#embedding-expressions-in-jsx)
- [Create functional and class components](https://reactjs.org/docs/components-and-props.html)
- [Pass data via props and set default props](https://reactjs.org/docs/components-and-props.html#props-are-read-only)
- [State and Lifecycle](https://reactjs.org/docs/state-and-lifecycle.html)
- [Explore basic lifecycle methods in class components](https://reactjs.org/docs/state-and-lifecycle.html#adding-lifecycle-methods-to-a-class)
- [Use useState to manage state in functional components](https://reactjs.org/docs/hooks-state.html)
- [Event Handling](https://reactjs.org/docs/handling-events.html)
- [Handle button clicks and form submissions](https://reactjs.org/docs/handling-events.html#passing-arguments-to-event-handlers)
- [Practice passing arguments to event handlers](https://reactjs.org/docs/handling-events.html#passing-arguments-to-event-handlers)
- [Implement conditional rendering in components](https://reactjs.org/docs/conditional-rendering.html)
- [Render a list of tasks and add keys to list items](https://reactjs.org/docs/lists-and-keys.html)
- [Create a form to add new tasks](https://reactjs.org/docs/forms.html)
- [Manage form input state](https://reactjs.org/docs/forms.html#controlled-components)
- [Style components using CSS classes and inline styles](https://reactjs.org/docs/faq-styling.html)


## Advanced Topics
- [Building and Using Reusable Component Libraries (axios, sweetalert, formik, bootstrap/tailwind)](https://reactjs.org/docs/reusable-components.html)
- [Forms and Validation / Error handling](https://reactjs.org/docs/forms.html#controlled-components)
- [Complex Forms and Validation](https://formik.org/)
- [Higher-Order Components (HOCs)](https://reactjs.org/docs/higher-order-components.html)
- [Context API](https://reactjs.org/docs/context.html)
- [Advanced State Management](https://redux.js.org/)
- [Side Effects and Data Fetching](https://reactjs.org/docs/hooks-effect.html)
- [Performance Optimization (React.memo, React.PureComponent, Code Splitting, and Lazy Loading)](https://reactjs.org/docs/optimizing-performance.html)
- [Advanced Performance Optimization](https://reactjs.org/docs/optimizing-performance.html#profiling-components-with-the-chrome-performance-tab)
- [GraphQL](https://graphql.org/)
- [Server-Side Rendering (SSR) with Next.js](https://nextjs.org/docs)
- [Animation in React](https://reactcommunity.org/react-transition-group/)




This comprehensive 4-hour training module ensures that students gain an in-depth understanding of React components, styling, and CRUD operations, with ample time for hands-on practice and advanced topics.

