#	====================		Colors			====================

RED = \033[0;31m
GREEN = \033[0;32m
BLUE = \033[0;34m
YELLOW = \033[0;33m
MAGENTA = \033[0;35m
CYAN = \033[0;36m

B_RED = \033[1;31m
B_GREEN = \033[1;32m
B_BLUE = \033[1;34m
L_BLUE = \033[1;94m
B_YELLOW = \033[1;33m
B_MAGENTA = \033[1;35m
B_CYAN = \033[1;36m

RESET = \033[0m

# ============================ {Directories} ============================

INC = includes

SRC = srcs
OBJ_DIR = objects

BONUS_SRC = srcs_bonus
BONUS_DIR = objects_bonus

# ============================ {Files      } ============================

NAME = so_long
TITLE = $(B_YELLOW)$(NAME)$(RESET):
FILES = so_long.c map.c utils.c flood_fill.c initializers.c texture_loader.c \
		rend.c move.c hook.c destroy.c
OBJ = $(FILES:.c=.o)
TARGET = $(addprefix $(OBJ_DIR)/, $(OBJ))

BONUS = so_long_bonus
BONUS_FILES = so_long_bonus.c map_bonus.c utils_bonus.c flood_fill_bonus.c \
			  initializers_bonus.c texture_loader_bonus.c rend_bonus.c \
			  move_bonus.c hook_bonus.c destroy_bonus.c enemy_bonus.c \
			  
BONUS_OBJ = $(BONUS_FILES:.c=.o)
BONUS_TARGET = $(addprefix $(BONUS_DIR)/, $(BONUS_OBJ))
B_TITLE = $(B_YELLOW)$(BONUS)$(RESET):

# ============================ {Commands   } ============================

CC = gcc
RM = rm

# ============================ {Flags      } ============================
W = -Wall -Wextra -Werror
O = -c
I = -I $(INC)
WBLOCK = --no-print-directory

LIBFT = -L ./libft -lft
MLX = -L ./minilibx-linux -lmlx -lXext -lX11

# ============================ {Rules      } ============================

all: $(NAME)

$(NAME): $(OBJ_DIR) $(TARGET)
	@make $(WBLOCK) -C ./libft
	@make $(WBLOCK) -C ./minilibx-linux
	@$(CC) $(W) $(TARGET) $(LIBFT) $(MLX) -o $(NAME)
	@printf "$(TITLE) $(GREEN)Program created.\n"

$(OBJ_DIR):
	@mkdir $(OBJ_DIR)

$(OBJ_DIR)/%.o: $(SRC)/%.c
	$(eval COMPTEUR=$(shell echo $$(($(COMPTEUR)+1))))
	@printf "\e[?25l"
	@if test $(COMPTEUR) -eq 1;then \
		printf "$(B_YELLOW)$(NAME)$(RESET):$(YELLOW) Compiling binary files...$(RESET)\n\n";fi
	@printf "\033[A\33[2K\r\t $(B_CYAN)Binary $(COMPTEUR):$(CYAN) $@$(RESET)\n"
	@$(CC) $(W) $(O) $(I) $< -o $@

clean:
	@make $(WBLOCK) clean -C ./libft
	@make $(WBLOCK) clean -C ./minilibx-linux
	@$(RM) -rf $(OBJ_DIR) $(BONUS_DIR)
	@printf "$(TITLE) $(RED)Binary files deleted.$(RESET)\n"

fclean:
	@make $(WBLOCK) fclean -C ./libft
	@$(RM) -rf $(NAME) $(BONUS)
	@$(RM) -rf $(OBJ_DIR) $(BONUS_DIR)
	@printf "$(TITLE) $(RED)Binary files deleted.$(RESET)\n"
	@printf "$(TITLE) $(RED)Program deleted.$(RESET)\n"

re: fclean all

bonus: $(BONUS)

$(BONUS): $(BONUS_DIR) $(BONUS_TARGET)
	@make $(WBLOCK) -C ./libft
	@make $(WBLOCK) -C ./minilibx-linux
	@$(CC) $(W) $(BONUS_TARGET) $(LIBFT) $(MLX) -o $(BONUS)
	@printf "$(B_TITLE) $(GREEN)Program created.\n"

$(BONUS_DIR):
	@mkdir $(BONUS_DIR)

$(BONUS_DIR)/%.o: $(BONUS_SRC)/%.c
	$(eval COMPTEUR=$(shell echo $$(($(COMPTEUR)+1))))
	@printf "\e[?25l"
	@if test $(COMPTEUR) -eq 1;then \
		printf "$(B_YELLOW)$(BONUS)$(RESET):$(YELLOW) Compiling binary files...$(RESET)\n\n";fi
	@printf "\033[A\33[2K\r\t       $(B_CYAN)Binary $(COMPTEUR):$(CYAN) $@$(RESET)\n"
	@$(CC) $(W) $(O) $(I) $< -o $@

test: $(BONUS)
	./so_long_bonus maps/bonus/medium.ber
	
re: fclean bonus

.PHONY: all clean fclean re

# ============================ {END        } ============================