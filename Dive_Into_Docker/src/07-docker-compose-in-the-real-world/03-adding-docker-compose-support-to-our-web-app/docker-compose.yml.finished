version: '3'

services:
  redis:
    image: 'redis:3.2-alpine'
    ports:
      - '6379:6379'
    volumes:
      - 'redis:/data'

  web:
    build: .
    depends_on:
      - 'redis'
    env_file:
      - '.env'
    ports:
      - '5000:5000'
    volumes:
      - '.:/app'

volumes:
  redis: {}
