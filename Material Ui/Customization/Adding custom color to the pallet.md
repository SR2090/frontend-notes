
```ts
import { ThemeProvider } from "@emotion/react";

import { createTheme } from "@mui/material";

import { BrowserRouter as Router, Route, Routes } from "react-router-dom";

import "./App.css";

import { RootLayout } from "./pages/RootLayout";

import { LoginComponent } from "./pages/LoginComponent";

import { SignUpComponent } from "./pages/SignUpComponent";

import OverviewPage from "./pages/OverviewPage";

import RootAuthenticatedPages from "./pages/RootAuthenticatedPages";

declare module '@mui/material/styles' {

  interface Palette {

    gray: Palette['primary'];

  }

  

  interface PaletteOptions {

    gray?: PaletteOptions['primary'];

  }

}

  

const theme = createTheme({

  palette: {

    gray: {

      main: '#696868',

      light: '#B3B3B3',

      dark: '#201F24',

      contrastText: '#F2F2F2',

    }

  },

});

  

function App() {

  return (

    <ThemeProvider theme={theme}>

      <Router>

        <Routes>

          {/* Root Layout with Nested Routes */}

          <Route path="/" element={<RootLayout />}>

            <Route path="login" element={<LoginComponent />} />

            <Route path="sign-up" element={<SignUpComponent />} />

          </Route>

  

          {/* Standalone Routes */}

          <Route path="/auth" element={<RootAuthenticatedPages />}>

            <Route path="overview" element={<OverviewPage />} />

          </Route>

        </Routes>

      </Router>

    </ThemeProvider >

  );

}

  

export default App;
```


Using module augmentation we introduce custom color and then use it to color our components.