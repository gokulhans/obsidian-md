
```jsx
import React from "react";
import ReactMarkdown from "react-markdown";
import rehypeRaw from "rehype-raw";
import remarkGfm from "remark-gfm";
import { Prism as SyntaxHighlighter } from "react-syntax-highlighter";
import {
  atomDark,
  a11yDark,
  darcula,
  dark,
  vsDark,
  vscDarkPlus,
} from "react-syntax-highlighter/dist/cjs/styles/prism";

export default function ExamplePage({ content }) {
  const [copyOk, setCopyOk] = React.useState(false);

  const handleCopy = (code) => {
    navigator.clipboard.writeText(code);
    setCopyOk(true);
    setTimeout(() => {
      setCopyOk(false);
    }, 500);
  };

  const Pre = ({ children }) => (
    <pre className="relative blog-pre">
      <button
        className="absolute top-0 right-0 p-1 mr-2 mt-1 text-gray-600 hover:text-gray-800 focus:outline-none"
        onClick={() => handleCopy(children.props.children)}
      >
        {!copyOk ? (
          <h4 className="bg-green-600 text-white rounded-lg px-3 font-medium">
            Copy
          </h4>
        ) : (
          <h4 className="bg-green-600 text-white rounded-lg px-3 font-medium">
            Copied
          </h4>
        )}
      </button>
      {children}
    </pre>
  );

  const renderers = {
    code: ({ node, inline, className = "", children, ...props }) => {
      const match = /language-(\w+)/.exec(className || "");
      return !inline && match ? (
        <SyntaxHighlighter
          style={vscDarkPlus}
          language={match[1]}
          PreTag="div"
          {...props}
        >
          {String(children).replace(/\n$/, "")}
        </SyntaxHighlighter>
      ) : (
        <code className={className} {...props}>
          {children}
        </code>
      );
    },
  };

  return (
    <div className="prose lg:prose-lg xl:prose-xl">
      <ReactMarkdown
        className="post-markdown prose"
        rehypePlugins={[rehypeRaw]}
        remarkPlugins={[remarkGfm]}
        components={{ pre: Pre, ...renderers }}
      >
        {content}
      </ReactMarkdown>
    </div>
  );
}
```