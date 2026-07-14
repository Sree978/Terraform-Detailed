will use it for reuse code and maintain infrstructure 
 way of organizing folders



 Dynamic block
  to reduce the code length

  envs
├── dev
│   ├── compute
│   │   ├── main.tf
│   │   ├── output.tf
│   │   └── variable.tf
│   ├── security
│   │   ├── main.tf
│   │   └── variable.tf
│   └── storage
│       ├── main.tf
│       └── variable.tf
├── prod
├── stage
└── modules
    └── main.tf
