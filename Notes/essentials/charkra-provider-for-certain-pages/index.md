//chakraWrapper component for certain pages.

import * as React from "react"
import {
  ChakraProvider,
  createSystem,
  defaultConfig,
} from "@chakra-ui/react";

const system = createSystem(defaultConfig, {
  preflight: false,
});

export default function ChakraWrapper({ children }) {
  return (
    <ChakraProvider value={system}>
      {children}
    </ChakraProvider>
  );
}