 # Why Do I Automatically Get 5 Ports in My Codespaces?

When you create a new Codespace, it automatically provisions a set of default ports. These ports are pre-configured to help streamline the development process by providing common services and tools that developers frequently use. Here are some reasons why you might see these ports:

1. **Development Servers**: Many development environments require servers to run on specific ports. For example, a web server might run on port 3000 or 8080.
2. **Database Connections**: Databases often run on specific ports, such as 5432 for PostgreSQL or 3306 for MySQL.
3. **Debugging Tools**: Debuggers and other development tools may use specific ports to communicate with your development environment.
4. **Pre-configured Services**: Codespaces might come with pre-configured services that require certain ports to be open for communication.

These default ports are intended to make it easier for you to start coding without needing to manually configure your environment each time.

If you need to customize the ports, you can do so in the `.devcontainer.json` file within your repository.

For more detailed information, you can refer to the [official documentation](https://docs.github.com/en/codespaces).
