# Using ROS Noetic Docker Template from:

Author: [Tobit Flatscher](https://github.com/2b-t) (2021 - 2024)

### Passo 1: Iniciar o Contêiner Docker
``bash
cd ros/
docker compose -f docker/docker-compose-gui.yml up -d
``
### Passo 2: Acessar o Terminal do Contêiner
``bash
cd ros/
docker exec -it ros_docker bash
``
### Passo 3: Habilitar Interfaces Gráficas (opcional)
``bash
xhost +
``
### Passo 4: Importar Repositórios
``bash
cd src/
vcs import < .repos
``
### Passo 5: Buildar o workspace

Duante a montagem da imagem já tem alguns alias configurados:
rsource = da source no devel/setup.bash
rbuild = builda com o catkin_build
rclean = limpa o ws removendo as pastas devel e build


RUN echo "alias rsource='source ${CATKIN_WORKSPACE_DIR}/devel/setup.bash'" >> /home/${USERNAME}/.bash_aliases \
 && echo "alias rbuild='(cd ${CATKIN_WORKSPACE_DIR} && catkin build)'" >> /home/${USERNAME}/.bash_aliases \
 && echo "alias rclean='(cd ${CATKIN_WORKSPACE_DIR} && catkin clean -y)'" >> /home/${USERNAME}/.bash_aliases \
 && echo "rsource || source /opt/ros/${ROS_DISTRO}/setup.bash" >> /home/${USERNAME}/.bashrc
