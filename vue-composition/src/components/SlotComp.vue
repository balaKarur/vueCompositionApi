<template>
    <div>
        <header>
           <slot name="header"></slot> 
        </header>
        <nav >
            <slot name="nav"></slot>
        </nav>
        <main >
            <slot name="main" ></slot>
            <slot  ></slot>
            <slot  ></slot>
           <div>
              Content
           </div>
        </main>
        <footer>
            <slot  name="footer"></slot>
        </footer>
    </div>
</template>