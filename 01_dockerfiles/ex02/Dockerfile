FROM ruby

RUN apt-get update && apt-get install -y nodejs
RUN gem install rails
RUN rails new /opt/app/hello_world
RUN cd /opt/app/hello_world
RUN rails generate controller pages

ONBUILD COPY . /opt/app
ONBUILD WORKDIR /opt/app
ONBUILD RUN bundle install
ONBUILD RUN exec rake db:migrate && rake db:seed

#
# docker build -t ft_rails .
# docker build -t ft_rails hello_world
# docker run -it --rm -p 3000:3000 ft_rails
#
