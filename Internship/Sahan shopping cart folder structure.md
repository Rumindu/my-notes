```
├── App.tsx
├── components
│   ├── AddToCart.tsx
│   ├── CartItem.tsx
│   ├── CartItemList.tsx
│   ├── CartItemSummary.tsx
│   ├── CategoryList.tsx
│   ├── CategoryTag.tsx
│   ├── CheckoutInfo.tsx
│   ├── CheckoutOrderSummary.tsx
│   ├── CheckoutShippingInfo.tsx
│   ├── Layout.tsx // page format
│   ├── MyOrderList.tsx
│   ├── Navbar.tsx
│   ├── OrderDetailsLeft.tsx
│   ├── OrderDetailsRight.tsx
│   ├── OrderListItem.tsx
│   ├── Pagination.tsx
│   ├── PersistAuth.tsx
│   ├── ProductCard.tsx
│   ├── ProductList.tsx
│   ├── ProtectedRoute.tsx
│   ├── shared
│   │   ├── Alert.tsx
│   │   └── Spinner.tsx
│   └── skeletons // For while content are  loading appearing Skelton of the page 
│       ├── CategoryTagSkeleton.tsx
│       ├── OrderSummaryItemSkeleton.tsx
│       └── ProductCardSkeleton.tsx
├── config
│   └── axios.ts
├── hooks
│   └── useAxiosPrivate.ts
├── index.css
├── main.tsx
├── pages
│   ├── CartPage.tsx
│   ├── CategoryProductsPage.tsx
│   ├── CheckoutPage.tsx
│   ├── HomePage.tsx
│   ├── MyOrdersPage.tsx
│   ├── OrderDetailsPage.tsx
│   ├── ProductDetailsPage.tsx
│   ├── SignInPage.tsx
│   └── SignUpPage.tsx
├── redux
│   ├── slices
│   │   ├── authSlice.ts
│   │   └── cartSlice.ts
│   └── store.ts
├── services
│   ├── authService.ts
│   ├── categoryService.ts
│   ├── orderService.ts
│   └── productService.ts
├── types.d.ts
├── utilities
│   ├── checkoutFormValidator.ts
│   ├── signInFormValidator.ts
│   ├── signUpFormValidator.ts
│   └── validator.ts
└── vite-env.d.ts
```